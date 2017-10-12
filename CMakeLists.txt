set(the_description "The ORB-SLAM2 module")
set(MODULE_NAME orbslam2)

ocv_add_module(orbslam2 opencv_core opencv_features2d opencv_calib3d WRAP js)

ocv_module_include_directories(
${PROJECT_SOURCE_DIR}
${PROJECT_SOURCE_DIR}/include
${PROJECT_SOURCE_DIR}/Thirdparty/DBoW2/DBoW2
${PROJECT_SOURCE_DIR}/Thirdparty/DBoW2/DUtils
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/g2o/core
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/g2o/solvers
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/g2o/stuff
${PROJECT_SOURCE_DIR}/Thirdparty/g2o/g2o/types
${PROJECT_SOURCE_DIR}/Thirdparty/eigen
)

# Check C++11 or C++0x support
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
   add_definitions(-DCOMPILEDWITHC11)
   message(STATUS "Using flag -std=c++11.")
elseif(COMPILER_SUPPORTS_CXX0X)
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
   add_definitions(-DCOMPILEDWITHC0X)
   message(STATUS "Using flag -std=c++0x.")
else()
   message(FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

SET(G2O_CXX_COMPILER "${CMAKE_CXX_COMPILER_ID} ${CMAKE_CXX_COMPILER}")
configure_file(${PROJECT_SOURCE_DIR}/Thirdparty/g2o/config.h.in ${PROJECT_SOURCE_DIR}/Thirdparty/g2o/config.h)

ocv_set_module_sources(
include/Converter.h    
include/Frame.h        
include/KeyFrameDatabase.h  
include/LocalMapping.h  
include/MapDrawer.h  
include/MapPoint.h   
include/ORBextractor.h  
include/ORBVocabulary.h  
include/Sim3Solver.h  
include/Tracking.h
include/FrameDrawer.h  
include/Initializer.h  
include/KeyFrame.h          
include/LoopClosing.h   
include/Map.h        
include/Optimizer.h  
include/ORBmatcher.h    
include/PnPsolver.h      
include/System.h      
include/Viewer.h
src/System.cc
src/Tracking.cc
src/LocalMapping.cc
src/LoopClosing.cc
src/ORBextractor.cc
src/ORBmatcher.cc
# src/FrameDrawer.cc
src/Converter.cc
src/MapPoint.cc
src/KeyFrame.cc
src/Map.cc
# src/MapDrawer.cc
src/Optimizer.cc
src/PnPsolver.cc
src/Frame.cc
src/KeyFrameDatabase.cc
src/Sim3Solver.cc
src/Initializer.cc
# src/Viewer.cc
# DBoW2
Thirdparty/DBoW2/DBoW2/BowVector.h
Thirdparty/DBoW2/DBoW2/FORB.h 
Thirdparty/DBoW2/DBoW2/FClass.h       
Thirdparty/DBoW2/DBoW2/FeatureVector.h
Thirdparty/DBoW2/DBoW2/ScoringObject.h   
Thirdparty/DBoW2/DBoW2/TemplatedVocabulary.h
Thirdparty/DBoW2/DUtils/Random.h
Thirdparty/DBoW2/DUtils/Timestamp.h
Thirdparty/DBoW2/DBoW2/BowVector.cpp
Thirdparty/DBoW2/DBoW2/FORB.cpp      
Thirdparty/DBoW2/DBoW2/FeatureVector.cpp
Thirdparty/DBoW2/DBoW2/ScoringObject.cpp
Thirdparty/DBoW2/DUtils/Random.cpp
Thirdparty/DBoW2/DUtils/Timestamp.cpp
# g2o
Thirdparty/g2o/g2o/types/types_sba.h
Thirdparty/g2o/g2o/types/types_six_dof_expmap.h
Thirdparty/g2o/g2o/types/types_sba.cpp
Thirdparty/g2o/g2o/types/types_six_dof_expmap.cpp
Thirdparty/g2o/g2o/types/types_seven_dof_expmap.cpp
Thirdparty/g2o/g2o/types/types_seven_dof_expmap.h
Thirdparty/g2o/g2o/types/se3quat.h
Thirdparty/g2o/g2o/types/se3_ops.h
Thirdparty/g2o/g2o/types/se3_ops.hpp
#core
Thirdparty/g2o/g2o/core/base_edge.h
Thirdparty/g2o/g2o/core/base_binary_edge.h
Thirdparty/g2o/g2o/core/hyper_graph_action.cpp
Thirdparty/g2o/g2o/core/base_binary_edge.hpp
Thirdparty/g2o/g2o/core/hyper_graph_action.h
Thirdparty/g2o/g2o/core/base_multi_edge.h           
Thirdparty/g2o/g2o/core/hyper_graph.cpp
Thirdparty/g2o/g2o/core/base_multi_edge.hpp         
Thirdparty/g2o/g2o/core/hyper_graph.h
Thirdparty/g2o/g2o/core/base_unary_edge.h          
Thirdparty/g2o/g2o/core/linear_solver.h
Thirdparty/g2o/g2o/core/base_unary_edge.hpp         
Thirdparty/g2o/g2o/core/marginal_covariance_cholesky.cpp
Thirdparty/g2o/g2o/core/base_vertex.h               
Thirdparty/g2o/g2o/core/marginal_covariance_cholesky.h
Thirdparty/g2o/g2o/core/base_vertex.hpp             
Thirdparty/g2o/g2o/core/matrix_structure.cpp
Thirdparty/g2o/g2o/core/batch_stats.cpp             
Thirdparty/g2o/g2o/core/matrix_structure.h
Thirdparty/g2o/g2o/core/batch_stats.h               
Thirdparty/g2o/g2o/core/openmp_mutex.h
Thirdparty/g2o/g2o/core/block_solver.h              
Thirdparty/g2o/g2o/core/block_solver.hpp            
Thirdparty/g2o/g2o/core/parameter.cpp               
Thirdparty/g2o/g2o/core/parameter.h                 
Thirdparty/g2o/g2o/core/cache.cpp                   
Thirdparty/g2o/g2o/core/cache.h
Thirdparty/g2o/g2o/core/optimizable_graph.cpp       
Thirdparty/g2o/g2o/core/optimizable_graph.h         
Thirdparty/g2o/g2o/core/solver.cpp                  
Thirdparty/g2o/g2o/core/solver.h
Thirdparty/g2o/g2o/core/creators.h                 
Thirdparty/g2o/g2o/core/optimization_algorithm_factory.cpp
Thirdparty/g2o/g2o/core/estimate_propagator.cpp     
Thirdparty/g2o/g2o/core/optimization_algorithm_factory.h
Thirdparty/g2o/g2o/core/estimate_propagator.h       
Thirdparty/g2o/g2o/core/factory.cpp                 
Thirdparty/g2o/g2o/core/optimization_algorithm_property.h
Thirdparty/g2o/g2o/core/factory.h                   
Thirdparty/g2o/g2o/core/sparse_block_matrix.h
Thirdparty/g2o/g2o/core/sparse_optimizer.cpp  
Thirdparty/g2o/g2o/core/sparse_block_matrix.hpp
Thirdparty/g2o/g2o/core/sparse_optimizer.h
Thirdparty/g2o/g2o/core/hyper_dijkstra.cpp 
Thirdparty/g2o/g2o/core/hyper_dijkstra.h
Thirdparty/g2o/g2o/core/parameter_container.cpp     
Thirdparty/g2o/g2o/core/parameter_container.h
Thirdparty/g2o/g2o/core/optimization_algorithm.cpp 
Thirdparty/g2o/g2o/core/optimization_algorithm.h
Thirdparty/g2o/g2o/core/optimization_algorithm_with_hessian.cpp 
Thirdparty/g2o/g2o/core/optimization_algorithm_with_hessian.h
Thirdparty/g2o/g2o/core/optimization_algorithm_levenberg.cpp 
Thirdparty/g2o/g2o/core/optimization_algorithm_levenberg.h
Thirdparty/g2o/g2o/core/jacobian_workspace.cpp 
Thirdparty/g2o/g2o/core/jacobian_workspace.h
Thirdparty/g2o/g2o/core/robust_kernel.cpp 
Thirdparty/g2o/g2o/core/robust_kernel.h
Thirdparty/g2o/g2o/core/robust_kernel_factory.cpp
Thirdparty/g2o/g2o/core/robust_kernel_factory.h
Thirdparty/g2o/g2o/core/robust_kernel_impl.cpp 
Thirdparty/g2o/g2o/core/robust_kernel_impl.h
#stuff
Thirdparty/g2o/g2o/stuff/string_tools.h
Thirdparty/g2o/g2o/stuff/color_macros.h 
Thirdparty/g2o/g2o/stuff/macros.h
Thirdparty/g2o/g2o/stuff/timeutil.cpp
Thirdparty/g2o/g2o/stuff/misc.h
Thirdparty/g2o/g2o/stuff/timeutil.h
Thirdparty/g2o/g2o/stuff/os_specific.c    
Thirdparty/g2o/g2o/stuff/os_specific.h
Thirdparty/g2o/g2o/stuff/string_tools.cpp
Thirdparty/g2o/g2o/stuff/property.cpp       
Thirdparty/g2o/g2o/stuff/property.h
)

ocv_create_module()

set_target_properties(${the_module} PROPERTIES COMPILE_FLAGS "-Wno-non-virtual-dtor")
