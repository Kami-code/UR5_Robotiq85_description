# UR5_description

Repository for UR5_robotiq85 URDF and launch files, which can be both used in pybullet and ROS. Models are downloaded from the [repo](https://github.com/ElectronicElephant/pybullet_ur5_robotiq), but the urdf downloaded contains ".." in filename, which ROS moveit urdf parser will throw an error.

## Table of Files

- [src]
	- [ur5_description] : a description package of ur5, containing the ur5_robotiq85 urdf and meshes.
	- [ur5_moveit_config] : a package created by moveit_setup_assistant, defining movegroup, collision matrix, etc. You also can create the config package using the urdf model in "ur5_description" by yourself.
	
	
## Notes

The packages files are arranged in ROS style, and can be easily compiled in ROS1-noetic. When we want to use the urdf in pybullet, bear in mind the pybullet urdf parser will automatically ignore "package://" and treat the remaining uri as relative filesystem path.([see here for similar behavior in GAZEBO](https://answers.gazebosim.org//question/1684/when-importing-a-urdf-model-how-are-package-uris-parsed/)) So we need to rearrange the hierarchy of ur5_description as following:

- [ur5_robotiq_85.urdf]
	- [moveit_resources_ur5_description] : the dirname is defined by the package name in urdf. If you want to rename the package in urdf, see CMakeLists.txt and package.xml and change them both with the corresponding name in urdf.
		- [meshes] : the models required by ur5_robotiq_85.urdf
		- [...] : others useless files in pybullet
