cmake_minimum_required(VERSION 3.1)

project(bit_humanoid)

find_package(catkin REQUIRED)

catkin_package()

# Configure the module file first
configure_file(module/module.yaml "${CMAKE_CURRENT_BINARY_DIR}/module/module.yaml")
# Now configure the alias in the HOME directory at a location where mc_rtc looks for aliases
configure_file(module/alias.yaml $ENV{HOME}/.config/mc_rtc/aliases/BITHumanoid.yaml)
configure_file(mujoco/bit_humanoid.yaml $ENV{HOME}/.config/mc_rtc/mc_mujoco/bit_humanoid.yaml)
foreach(dir config launch meshes urdf)
	install(DIRECTORY ${dir}/
		DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)
