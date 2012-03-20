mqo.three.js
============
mqo.three.js is a mqo parser for three.js.

Usage
-----
<!doctype html>
<html>
  <head>
    <meta charset="UTF-8" />
    <script src="js/Three.js"></script>
    <script src="mqo.three.js"></script>
    <style>
      body {
        margin: 0px;
        background: #C0C0C0;
        overflow: hidden;
      };
    </style>
    <script>
      window.addEventListener('load', function() {
        var camera, scene, renderer, trackball, meshes;

        MqoLoader.load({
          url : 'assets/geometry.mqo'
          , MaterialConstructor : THREE.MeshPhongMaterial
          , texturePath : 'assets'
          , callback : function(out) {
              meshes = out;
              init();
              animate();
          }
        });

        var init = function() {
          scene = new THREE.Scene();

          camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 1, 100 );
          camera.position.z = 5;
          scene.add( camera );

          scene.add( new THREE.DirectionalLight(0x7f7f7f));
          scene.add( new THREE.AmbientLight(0xc0c0c0));

          var axis =  new THREE.AxisHelper();
          axis.scale.x = 0.01;
          axis.scale.y = 0.01;
          axis.scale.z = 0.01;
          scene.add(axis);

          for(var i = 0; i < meshes.length; ++i) {
            scene.add( meshes[i] );
          }

          renderer = new THREE.WebGLRenderer();
          renderer.setSize( window.innerWidth, window.innerHeight );

          trackball = new THREE.TrackballControls(camera, renderer.domElement);

          document.body.appendChild( renderer.domElement );
        }

        var animate = function() {
          trackball.update()

          requestAnimationFrame(animate);
          render();
        }

        var render = function () {
          renderer.render( scene, camera );
        }
      }, false);
    </script>
  </head>
</html>

