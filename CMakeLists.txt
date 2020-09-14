cmake_minimum_required (VERSION 3.14)

project (superbible7)

find_package(glfw3 CONFIG REQUIRED)
find_package(OpenGL REQUIRED)

if(NOT OPENGL_FOUND)
    message(ERROR " OPENGL not found!")
endif(NOT OPENGL_FOUND)

add_library(sb7
            src/sb7/sb7.cpp
            src/sb7/sb7color.cpp
            src/sb7/sb7ktx.cpp
            src/sb7/sb7object.cpp
            src/sb7/sb7shader.cpp
            src/sb7/sb7textoverlay.cpp
            src/sb7/gl3w.c
)
target_include_directories(sb7 PUBLIC include/)
target_link_libraries(sb7 PUBLIC glfw)


set(EXAMPLES
  alienrain
  basicfbo
  bindlesstex
  blendmatrix
  blinnphong
  bumpmapping
  clipdistance
  csflocking
  compressrgtc
  cubemapenv
  cubicbezier
  cullindirect
  deferredshading
  depthclamp
  dflandscape
  dispmap
  dof
  envmapsphere
  equirectangular
  fontdemo
  fragcolorfrompos
  fragmentlist
  grass
  gsculling
  gslayered
  gsquads
  gstessellate
  hdrbloom
  hdrexposure
  hdrtonemap
  hqfilter
  indexedcube
  indirectmaterial
  instancedattribs
  julia
  ktxview
  linesmooth
  mirrorclampedge
  movingtri
  msaanative
  multidrawindirect
  multiscissor
  multiviewport
  noperspective
  normalviewer
  objectexploder
  ompparticles
  packetbuffer
  perpixelgloss
  phonglighting
  polygonsmooth
  prefixsum
  pmbfractal
  pmbstreaming
  prefixsum2d
  programinfo
  raytracer
  rimlight
  sampleshading
# sb6mrender
  sdfdemo
  shadowmapping
  shapedpoints
  simpleclear
  simpletexcoords
  simpletexture
  singlepoint
  singletri
  sparsetexture
  spinnycube
  springmass
  ssao
  starfield
  stereo
  subroutines
  tessellatedcube
  tessellatedgstri
  tessellatedtri
  tessmodes
  tesssubdivmodes
  toonshading
  tunnel
  wrapmodes
)

find_package(OpenMP REQUIRED)


foreach(EXAMPLE ${EXAMPLES})
  add_executable(${EXAMPLE} WIN32 src/${EXAMPLE}/${EXAMPLE}.cpp)
  target_link_libraries(${EXAMPLE} PRIVATE sb7 ${OPENGL_LIBRARIES} OpenMP::OpenMP_CXX)
  
endforeach(EXAMPLE)