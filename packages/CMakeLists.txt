cmake_minimum_required(VERSION 3.9)


include(CMakeDependentOption)

# select on which OS python must run
set(pyplatformList windows linux)
set(pyplatform Green CACHE STRING "Status of something")
set_property(CACHE pyplatform PROPERTY STRINGS ${pyplatformList})
if(NOT pyplatform IN_LIST pyplatformList)
    message(FATAL_ERROR "pyplatform must be one of ${pyplatformList}")
endif() 

 
#select the architecture
set(pyarchList 32 64)
set(pyarch Green CACHE STRING "Status of something")
set_property(CACHE pyarch PROPERTY STRINGS ${pyarchList})
if(NOT pyarch IN_LIST pyarchList)
    message(FATAL_ERROR "pyarch must be one of ${pyarchList}")
endif() 
 
  
#set location of where python is
set(py_exe "C:\\python\\Python38-64\\python.exe")
set(py_exe "path to pyton.exe required" CACHE STRING "Status of something")


file( GLOB server_py pypiserver*.* )
MESSAGE( "The server install canidate list ${server_py}")

 
file(WRITE ${CMAKE_CURRENT_SOURCE_DIR}/.ENV "TAG=${docker_tag}")
 
set(TEX_DOC_BASE document)

add_custom_target( 
    py_download
    COMMAND docker compose up
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)
 
add_custom_target(
    py_server_setup
    COMMAND ${py_exe} -m venv virt_env
    COMMAND virt_env\\Scripts\\activate.bat && pip install  ${server_py} && virt_env\\Scripts\\deactivate.bat
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
) 

add_custom_target(
    py_server_run
    COMMAND  START  /B cmd /c "virt_env\\Scripts\\activate.bat && pypi-server run -p 1234 .  && virt_env\\Scripts\\deactivate.bat"
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
) 

add_custom_target(
    py_install
    COMMAND virt_env\\Scripts\\activate.bat && pip install -r requirements.txt --index-url http://localhost:1234/ && virt_env\\Scripts\\deactivate.bat
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

# https://gitlab.kitware.com/cmake/community/-/wikis/FAQ#how-do-i-use-cmake-to-build-latex-documents
# https://cmake.org/cmake/help/latest/command/add_custom_command.html


 