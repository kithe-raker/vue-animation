<template>
  <div></div>
</template>

<script>
import "pathseg";
import Matter from "matter-js";

const paths = [
  "M289.05,84.63L98.225,308.136c-6.35,7.44-9.126,17.291-7.594,26.954l10.514,66.144c1.32,8.312,8.484,14.441,16.901,14.44h66.971c9.785,0,19.079-4.283,25.434-11.725l206.015-241.29c5.93-6.943,5.104-17.379-1.841-23.305l-42.83-36.57c-6.946-5.928-17.38-5.104-23.31,1.837l-152.4,178.477c-3.312,3.872-1.941,7.557-0.754,15.562c0.647,4.358,4.409,7.572,8.817,7.528c8.201-0.082,11.959,0.677,15.254-3.186l104.745-122.653l30.031,25.641l-108.396,126.93c-5.823,6.821-14.307,10.795-23.272,10.904h-40.639c-10.349,0.124-19.191-6.943-20.691-17.18l-5.896-40.215c-1.304-8.875,1.292-17.878,7.118-24.697L321.757,75.111c18.261-21.39,50.409-23.929,71.803-5.664l50.576,43.18c21.395,18.265,23.932,50.414,5.666,71.806L235.457,435.479c-10.447,12.243-25.735,19.284-41.83,19.271h-89.321c-19.688-0.012-36.449-14.382-39.549-33.821l-14.072-88.213c-2.53-15.89,2.027-32.097,12.479-44.339L259.017,58.988L289.05,84.63z",
];

export default {
  name: "PhysicsBox",
  mounted() {
    this.initWorld();
  },
  methods: {
    initWorld() {
      let height = window.innerHeight,
        width = window.innerWidth;

      var Engine = Matter.Engine,
        Render = Matter.Render,
        Runner = Matter.Runner,
        Common = Matter.Common,
        MouseConstraint = Matter.MouseConstraint,
        Mouse = Matter.Mouse,
        World = Matter.World,
        Vertices = Matter.Vertices,
        Svg = Matter.Svg,
        Bodies = Matter.Bodies;

      // create engine
      var engine = Engine.create(),
        world = engine.world;

      // create renderer
      var render = Render.create({
        element: this.$el,
        engine: engine,
        options: {
          width: width,
          height: height,
          // pixelRatio: 'auto',
          wireframes: false,
          showDebug: false,
          showBroadphase: false,
          showBounds: false,
          showVelocity: false,
          showCollisions: false,
          showSeparations: false,
          showAxes: false,
          showPositions: false,
          showAngleIndicator: false,
          showIds: false,
          showShadows: false,
          showVertexNumbers: false,
          showConvexHulls: false,
          showInternalEdges: false,
          showMousePosition: false,
        },
      });

      Render.run(render);

      // create runner
      var runner = Runner.create();
      Runner.run(runner, engine);

      var vertexSets = [],
        color = Common.choose([
          "#556270",
          "#4ECDC4",
          "#C7F464",
          "#FF6B6B",
          "#C44D58",
        ]);

      paths.forEach((path, i) => {
        var newElement = document.createElementNS(
          "http://www.w3.org/2000/svg",
          "path"
        );
        newElement.setAttribute("d", path);

        console.log(newElement);

        var points = Svg.pathToVertices(newElement, 30);
        vertexSets.push(Vertices.scale(points, 0.4, 0.4));

        World.add(
          world,
          Bodies.fromVertices(
            100 + i * 150,
            200 + i * 50,
            vertexSets,
            {
              render: {
                fillStyle: color,
                strokeStyle: color,
                lineWidth: 1,
              },
            },
            true
          )
        );
      });

      World.add(world, [
        // top
        Bodies.rectangle(width / 2, -50, width, 100, {
          isStatic: true,
        }),
        // bottom
        Bodies.rectangle(width / 2, height + 50, width, 100, {
          isStatic: true,
        }),
        // left
        Bodies.rectangle(-50, height / 2, 100, height, { isStatic: true }),
        // right
        Bodies.rectangle(width + 50, height / 2, 100, height, {
          isStatic: true,
        }),

        // // right
        // Bodies.rectangle(900, 300, 100, 600, { isStatic: true }),
        // // top
        // Bodies.rectangle(400, -50, 1000, 100, { isStatic: true }),
        // // bottom
        // Bodies.rectangle(400, 650, 1000, 100, { isStatic: true }),

        // item
        // Bodies.rectangle()
      ]);

      // add mouse control
      var mouse = Mouse.create(render.canvas),
        mouseConstraint = MouseConstraint.create(engine, {
          mouse: mouse,
          constraint: {
            stiffness: 0.8,
            render: {
              visible: false,
            },
          },
        });

      World.add(world, mouseConstraint);

      // keep the mouse in sync with rendering
      render.mouse = mouse;

      render.canvas.style.backgroundColor = "#fff";

      // fit the render viewport to the scene
      Render.lookAt(render, {
        min: { x: 0, y: 0 },
        max: {
          x: window.innerWidth,
          y: window.innerHeight,
        },
      });
    },
  },
};
</script>