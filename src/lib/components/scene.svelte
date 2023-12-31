<script>
  // @ts-nocheck
  import { afterUpdate, onMount } from "svelte";
  import {
    PerspectiveCamera,
    WebGLRenderer,
    Scene,
    Color,
    Group,
    BoxGeometry,
    MeshStandardMaterial,
    Mesh,
    PointLight,
    Vector2,
    LOD,
  } from "three";
  import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
  import { EffectComposer } from "three/examples/jsm/postprocessing/EffectComposer.js";
  import { RenderPass } from "three/examples/jsm/postprocessing/RenderPass.js";
  import { ShaderPass } from "three/examples/jsm/postprocessing/ShaderPass.js";
  import { UnrealBloomPass } from "three/addons/postprocessing/UnrealBloomPass.js";
  import { PixelShader } from "./PixelShader";
  import seedrandom from "seedrandom";

  export let input;
  export let isPremium = false;
  export let isVip = false;

  let rng = seedrandom(input);
  let canvas;
  let renderer;
  let camera;
  let scene;
  let controls;
  let structure;
  let composer;
  let frameId;

  let numBoxes = 320 + Math.floor(rng() * 20 - 10);
  let baseDistance = 0.035 + rng() * 0.005 - 0.0025;
  let radius = 0.96 + rng() * 0.04 - 0.02;
  let turns = 5 + Math.floor(rng() * 2 - 1);
  let angleStep = (turns * Math.PI * 2) / numBoxes;
  let boxHeight = 0.05;
  let boxWidth = boxHeight * 15;
  let boxDepth = boxHeight * 1;
  let pixelFactor = 1;
  let lightCount = 100;
  const lightIntensity = isPremium ? 1 : 0.4 + rng() * 0.1 - 0.05;
  const lightDistance = 5000 + rng() * 1000 - 500;
  let inputRGV;
  let boxColor = "#dffe00";
  let neonColors = ["#000000", "#494949", "#d2d0cb"];

  let boxesLeft;
  let boxesRight;
  let lod = new LOD();

  $: if (input) {
    rng = seedrandom(input);

    numBoxes = 300 + Math.floor(rng() * 20 - 10);
    baseDistance = 0.035 + rng() * 0.005 - 0.0025;
    radius = 0.96 + rng() * 0.04 - 0.08;
    turns = 5 + Math.floor(rng() * 2 - 1.4);
    angleStep = (turns * Math.PI * 2) / numBoxes;
    pixelFactor = 1 + Math.floor(rng() * 8);
    updateHelixAndLights();
  }

  function updateHelixAndLights() {
    if (scene && structure) {
      scene.remove(structure);
      structure = createBoxesAlongHelix();
      scene.add(structure);
      if (boxesLeft) {
        scene.remove(boxesLeft);
      }
      if (boxesRight) {
        scene.remove(boxesRight);
      }
      boxesLeft = createBoxPattern("left");
      boxesRight = createBoxPattern("right");
      scene.add(boxesLeft);
      scene.add(boxesRight);
    }

    scene.children = scene.children.filter(
      (child) => !(child instanceof PointLight)
    );

    // Add different levels of detail to the LOD object
    const highDetail = createBoxesAlongHelix(); // High detail
    const mediumDetail = createMediumDetail(); // Medium detail (implement this function)
    const lowDetail = createLowDetail(); // Low detail (implement this function)

    lod.addLevel(highDetail, 0);
    lod.addLevel(mediumDetail, 100); // Adjust the distance as needed
    lod.addLevel(lowDetail, 200); // Adjust the distance as needed

    lod.updateMatrixWorld(); // Update LOD matrices
    scene.add(lod);

    const lightIntensity = 0.4 + rng() * 0.1 - 0.05;
    const lightDistance = 5000 + rng() * 1000 - 500;

    for (let colorIndex = 0; colorIndex < 30; colorIndex++) {
      const color = new Color(neonColors[colorIndex]);
      // for (let i = 0; i < lightCount / neonColors.length; i++) {
      const light = new PointLight(color, lightIntensity, lightDistance);
      light.position.set(
        (rng() - 0.5) * radius * 2,
        rng() * numBoxes * baseDistance - ((numBoxes - 1) * baseDistance) / 2,
        (rng() - 0.5) * radius * 2
      );
      scene.add(light);
      // }
    }
  }
  function createMediumDetail() {
    // Implement medium detail geometry here
    const geometry = new BoxGeometry(0.5, 0.05, 0.1);
    const material = new MeshStandardMaterial({
      color: boxColor,
      metalness: 0,
      roughness: 1,
    });
    const mesh = new Mesh(geometry, material);
    return mesh;
  }

  function createLowDetail() {
    // Implement low detail geometry here
    const geometry = new BoxGeometry(0.2, 0.05, 0.1);
    const material = new MeshStandardMaterial({
      color: boxColor,
      metalness: 0,
      roughness: 1,
    });
    const mesh = new Mesh(geometry, material);
    return mesh;
  }
  onMount(() => {
    init();
    animate();

    if (isPremium && !isVip) {
      renderer.setClearColor(new Color("rgb(2, 2, 2)"));
      boxColor = "#494949";
      neonColors = ["#000000", "#494949", "#d2d0cb"];
      updateHelixAndLights();
    } else if (!isPremium && isVip) {
      renderer.setClearColor(new Color("#dffe00"));
      updateHelixAndLights();
    }

    // return () => {
    //   structure.traverse((object) => {
    //     if (object.geometry) object.geometry.dispose();
    //     if (object.material) object.material.dispose();
    //   });
    //   cancelAnimationFrame(frameId);
    //   renderer.dispose();
    //   controls.dispose();
    //   composer.dispose();
    //   scene.clear();
    // };
    return () => {
      // Dispose of Three.js objects
      structure.traverse((object) => {
        if (object.geometry) object.geometry.dispose();
        if (object.material) object.material.dispose();
      });
      cancelAnimationFrame(frameId);
      renderer.dispose();
      controls.dispose();
      composer.dispose();
      scene.clear();
      if (structure) {
        structure.traverse((child) => {
          if (child instanceof THREE.Mesh) {
            // Dispose of geometry and materials
            child.geometry.dispose();
            child.material.dispose();
          }
        });
        scene.remove(structure);
      }

      if (boxesLeft) {
        boxesLeft.traverse((child) => {
          if (child instanceof THREE.Mesh) {
            // Dispose of geometry and materials
            child.geometry.dispose();
            child.material.dispose();
          }
        });
        scene.remove(boxesLeft);
      }

      if (boxesRight) {
        boxesRight.traverse((child) => {
          if (child instanceof THREE.Mesh) {
            // Dispose of geometry and materials
            child.geometry.dispose();
            child.material.dispose();
          }
        });
        scene.remove(boxesRight);
      }

      cancelAnimationFrame(frameId);

      // Dispose of renderer and controls
      if (renderer) {
        renderer.dispose();
      }
      // if (controls) {
      //   controls.dispose();
      // }

      // Clear the scene
      if (scene) {
        scene.traverse((child) => {
          if (child instanceof THREE.Mesh) {
            // Dispose of geometry and materials
            child.geometry.dispose();
            child.material.dispose();
          }
        });
        scene.clear();
      }
    };
  });

  function createBoxesAlongHelix() {
    const structure = new Group();

    for (let i = 0; i < numBoxes; i++) {
      const theta = angleStep * i;
      const x = radius * Math.sin(theta);
      const y = i * baseDistance;
      const z = radius * Math.cos(theta);

      const boxGeometry = new BoxGeometry(boxWidth, boxHeight, boxDepth);
      const boxMaterial = new MeshStandardMaterial({
        color: boxColor,
        metalness: 0,
        roughness: 1,
      });

      const box = new Mesh(boxGeometry, boxMaterial);
      box.position.set(x, y, z);
      box.castShadow = true;
      box.receiveShadow = true;

      structure.add(box);
    }

    structure.position.y = -((numBoxes - 1) * baseDistance) / 2;
    return structure;
  }

  function addRandomLights() {
    for (let colorIndex = 0; colorIndex < neonColors.length; colorIndex++) {
      const color = new Color(neonColors[colorIndex]);
      for (let i = 0; i < lightCount / neonColors.length; i++) {
        const light = new PointLight(color, lightIntensity, lightDistance);
        light.position.set(
          (rng() - 0.5) * radius * 2,
          rng() * numBoxes * baseDistance - ((numBoxes - 1) * baseDistance) / 2,
          (rng() - 0.5) * radius * 2
        );
        scene.add(light);
      }
    }
  }

  function createBoxPattern(side) {
    const pattern = new Group();
    const count = Math.floor(6 + rng() * 60);
    const size = 0.02 + rng() * 0.02;
    const separation = size * 0.5;
    const directionMultiplier = side === "left" ? -1 : 1;

    const safeDistanceFromHelix = radius + size;

    for (let i = 0; i < count; i++) {
      const boxGeometry = new BoxGeometry(size, size, size);
      const boxMaterial = new MeshStandardMaterial({ color: boxColor });
      const box = new Mesh(boxGeometry, boxMaterial);

      let posX = directionMultiplier * safeDistanceFromHelix;
      let posY =
        rng() * numBoxes * baseDistance - ((numBoxes - 1) * baseDistance) / 2;
      let posZ = 0;
      let theta =
        ((posY + ((numBoxes - 1) * baseDistance) / 2) / baseDistance) *
        angleStep;
      let helixX = radius * Math.sin(theta);

      if (side === "left") {
        while (posX > helixX - size) {
          posY -= separation;
          theta =
            ((posY + ((numBoxes - 1) * baseDistance) / 2) / baseDistance) *
            angleStep;
          helixX = radius * Math.sin(theta);
        }
      } else {
        while (posX < helixX + size) {
          posY -= separation;
          theta =
            ((posY + ((numBoxes - 1) * baseDistance) / 2) / baseDistance) *
            angleStep;
          helixX = radius * Math.sin(theta);
        }
      }

      box.position.set(posX, posY, posZ);
      pattern.add(box);
    }

    return pattern;
  }

  function init() {
    scene = new Scene();
    camera = new PerspectiveCamera(
      75,
      canvas.clientWidth / canvas.clientHeight,
      0.1,
      1000
    );
    camera.frustumCulled = true;
    renderer = new WebGLRenderer({ canvas, antialias: true, alpha: true });
    renderer.setSize(canvas.clientWidth, canvas.clientHeight);
    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setClearColor(new Color("#000"));
    controls = new OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;
    controls.dampingFactor = 0.05;
    controls.maxPolarAngle = Math.PI;

    renderer.shadowMap.enabled = true;
    renderer.shadowMap.type = WebGLRenderer.PCFSoftShadowMap;

    // addRandomLights();

    structure = createBoxesAlongHelix();
    scene.add(structure);

    boxesLeft = createBoxPattern("left");
    boxesRight = createBoxPattern("right");
    scene.add(boxesLeft);
    scene.add(boxesRight);

    camera.position.z = 3.1;

    composer = new EffectComposer(renderer);
    const renderPass = new RenderPass(scene, camera);
    composer.addPass(renderPass);

    const pixelPass = new ShaderPass(PixelShader);
    pixelPass.uniforms["resolution"].value = new Vector2(
      canvas.clientWidth * 1,
      canvas.clientHeight * 1
    );
    pixelPass.uniforms["pixelSize"].value = pixelFactor;
    composer.addPass(pixelPass);

    const bloomPass = new UnrealBloomPass({
      threshold: 0.02,
      strength: 0.02,
      radius: 0.02,
      exposure: 0.1,
    });

    if (isPremium) {
      composer.addPass(pixelPass);
    } else if (isPremium) {
      composer.addPass(pixelPass);
    }
  }

  function animate() {
    frameId = requestAnimationFrame(animate);
    controls.update();
    composer.render();
  }
</script>

<canvas
  bind:this={canvas}
  style="background-color: {isPremium ? '#D1F544' : '#000'}"
  width="600"
  height="600"
/>
