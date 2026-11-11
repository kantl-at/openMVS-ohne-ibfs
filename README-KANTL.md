# OpenMVS without IBFS

This branch (`ohne-ibfs`) is a **modified version of OpenMVS** (AGPL-3.0). It is the source code of the program
kantl runs on its own processing servers to build 3D meshes from drone imagery.

## Base

- OpenDroneMap/WebODM fork: https://github.com/WebODM/openMVS, commit
  `988e582f94919408beefd88efc782ba97f6d15ff` (branch `355`), as built by ODX 3.8.4
  (`SuperBuild/cmake/External-OpenMVS.cmake`).
- Upstream: https://github.com/cdcseacave/openMVS

## Changes (notice under AGPL-3.0, section 5 a)

Modified by kantl on 2026-11-11:

- `libs/MVS/SceneReconstruct.cpp`: the line `#define DELAUNAY_MAXFLOW_IBFS` is disabled, so ReconstructMesh uses the
  Boost graph cut (Boykov-Kolmogorov) instead of IBFS.
- `libs/Math/IBFS` removed.

Reason: the IBFS license permits research use only. Nothing else is changed; the commit on this branch contains the
complete modification.

## Building

As OpenMVS itself. kantl builds with CMake (`-DOpenMVS_USE_CUDA=OFF -DOpenMVS_USE_OPENGL=OFF
-DOpenMVS_USE_PYTHON=OFF`), VCG (https://github.com/WebODM/VCG, `3fe55c6f`) and Eigen
(https://gitlab.com/libeigen/eigen, `7176ae16`).

## License

AGPL-3.0, see `LICENSE` (unchanged from OpenMVS). Third-party components keep their own licenses.
