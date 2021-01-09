# Three.js learning
This repository is made for me to copy right what I learn in three.js

**How to run**
```
cmd => http-server --port 3000
```
[Click here to view your page (localhost)](http://127.0.0.1:3000)

## Chapter 1
Learn how to run basic scene of three.js:
- Create scene, camera and object
- Add Plane, Cube and Sphere to Scene
- Add Light to the scene, target cast and receive shadow for the object when having Light
- Using couple of helper library like dat.GUI for creating control user interface, add stats library to see fps of object.
- Adding interval animation for object.

## Chapter 2. Basic Components that make up a Three.js Scene

### Creating a scene
We saw that for a scene to show anything, we need three types of components:
- Camera: This determines what is rendered on the screen
- Lights: These have an effect on how materials are shown and used when creating shadow effects
- Objects: These are the main objects that are rendered  from the perspective of the camera: cubes, spheres and the like

### Using the overrideMaterial property

the last property we discuss for the scene is **overrideMaterial**. When you use this property, all the objects in the scene will use the material that is set to the overrideMaterial property and  ignore the material that is set on the object itself.

In this section, we looked at the first of the core concepts of Three.js: THREE.Scene. The most important thing to remember about the scene is that it is basically a container for all the objects, lights, and cameras you  want to use when rendering. the following table summaries  the most important functions and attributes of the THREE.Scene object:

- add(object): This is used to add an object to the scene. You can also use this function,, as we'll see later on, to create groups of objects.
- children: this returns a list of all the objects that have been added to the scene, including the camera and lights.
- getObjectByName(name, recursive): When you create an object, you can give it a distinct name. The scene object has a function that you can use to directly retun an object with a specific name. If you set the recursive argument to  true, Three.js will also search through the complete tree of objects to find the object with the  specified name.
- remove(object): If you have a reference to an object in the scene, you can also remove it from the scene using this function.
- traverse(function): The children property returns a list of all the children in the scene. With the traverse function, we can also access these children. WIth reverse, all the children are passed in to the supplied function one by one.
- fog: This property allows you to set the fog for the scene. The fog will render a haze that hides faraway objects.
- overrideMaterial: With this property, you can force all the objects in the scene to use the same material.

### Tips
We used createMultiMaterialObject from the THREE.SceneUtils object to add a wireframe to the geometry we created. Three.js also provides an alternative way of adding a wireframe using THREE.WireframeHelper. To use this helper, first instantiate the helper like this:

**var helper = new THREE.WireframeHelper(mesh, 0x000000)**

You provide the mesh you want to show the wire frame for and the color of the wire frame. Three.js will now create a helper object that you can add to the scene, scene.add(helper). Since this helper internally is just a THREE.Line object, you can style how the wireframe appears. For instance, to set the width of the wireframe lines, use helper.material.linewidth = 2;

### Function and attributes for meshes
There are a couple  of properties that you can use to change where and how this mesh appears on the scene. We'll look at the following set of properties and functions:
- position: This determines the position of this object relative to the position of its parent. Most often, the parent of an object is a THREE.Scene object or a THREE.Object3D object.
- rotation: With this property, you can set the rotation of an object around any of its axis. Three.js also provides specific function for rotation around an axis: rotateX(), rotateY() and rotateZ().
- scale: This property allows you to scale the object around its x, y and z axes.
- translateX(amount), translateY(amount) and translateZ(amount): This property moves the object to the suitable axis. For the translate function,  you could also use the *translateOnAxis( axis, distance )* function, which allows you to translate the mesh a distance along a specific axis.
- visible: If you set this property to false, THREE.Mesh won't be rendered by Three.js


### Different camera for different uses
There is a difference in the way we create the camera. Let's look at THREE.PerspectiveCamera first, this camera takes the following arguments:

- fov: FOV stands for Field Of View. This is the part of the scene that can be seen from the position of the camera. Humans, for instance, have an almost 180-degree FOV, while some birds might even have a complete 360-degree FOV. But since a normal computer screen doesn't completely fill our vision, normally a smaller value is chosen. Most often, for games, a FOV between 60 and 90 degrees is chosen. **Good default: 50**
- aspect: This is the aspect ratio between the horizontal and vertical sizes of the area where we're to render the output. In our case, since we use the entire window, we just use that ratio. The aspect ratio determines the difference between the horizontal FOV and the vertical FOV. **Good default: window.innerWidth/window.innerHeight**.
- near: The near property defines from how close to the camera Three.js should render the scene. Normally, we set this to a very small value to directly render everything from the position of the camera. **Good default: 0.1**
- far: The far property defines how far the camera can see from the position of the camera. If we set this too low, a part of our scene might not be rendered, and if we set it too high, in some cases, it might affect the rendering performance. **Good default: 1000**
- zoom: The zoom property allows you to zoom in and out of the scene. When you see a number lower than 1, you zoo out of the scene, and if you use a number highter than 1, you zoom in. Note that if you specify a negative value, the scene will be rendered upside down. **Good default value: 1**

To configure the orthographic camera, we need to use other properties. The orthographic projection isn't interested either in the aspect ratio to use or with what FOV we look at the scene since all the objects are rendered at the same size. What you so when you define an orthographic camera is define the cuboid area that needs to be rendered. The properties for the orthographic camera reflect this, as follow:
- left: This is described in the Three.js documentation as Camera frustum left plane. You should see this as what is the left-hand border of what will be rendered. If you set this value to -100, you won't see any objects that are farther to the left-hand side.
- right: Same left property
- top
- bottom
- near
- far
- zoom

### Summary chapter 2
We showed all the functions and properties of THREE.Scene and explained how you can use these properties to configure yourr main scene. We also showed how you can create geometries. You can either create them from scratch using a THREE.Geometry object or use any of the built-in geometries Three.js provides. Finally, we showed how you can configure the 2 cameras Three.js provides. THREE.PerpectiveCamera renders a scene using a real-world perspective, and THREE.OrthographicCamera provides a fake 3D effect also often seen in games. 