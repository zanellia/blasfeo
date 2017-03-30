cmake_minimum_required(VERSION 2.8.11)
project(blasfeo)

# source files
file(GLOB BLASFEO_AUXILIARY_C99_SRC
	# double precision
	${PROJECT_SOURCE_DIR}/auxiliary/d_aux_lib4.c
	${PROJECT_SOURCE_DIR}/auxiliary/c99/kernel_dgecp_lib4.c
	${PROJECT_SOURCE_DIR}/auxiliary/c99/kernel_dgetr_lib4.c
	# single precision
	${PROJECT_SOURCE_DIR}/auxiliary/c99/s_aux_lib4.c
	${PROJECT_SOURCE_DIR}/auxiliary/c99/s_aux_extern_depend_lib4.c
	)

file(GLOB BLASFEO_KERNELS_SRC
	# double precision
	${PROJECT_SOURCE_DIR}/kernel/c99/kernel_dgemm_4x4_lib4.c
	${PROJECT_SOURCE_DIR}/kernel/c99/kernel_dgemm_diag_lib4.c
	${PROJECT_SOURCE_DIR}/kernel/c99/kernel_dgemv_4_lib4.c
	${PROJECT_SOURCE_DIR}/kernel/c99/kernel_dsymv_4_lib4.c
	${PROJECT_SOURCE_DIR}/kernel/c99/kernel_dgetrf_pivot_4_lib4.c
	# single precision
	${PROJECT_SOURCE_DIR}/kernel/c99/kernel_sgemm_4x4_lib4.c
	${PROJECT_SOURCE_DIR}/kernel/c99/kernel_sgemv_4_lib4.c)

file(GLOB BLASFEO_BLAS_SRC
	# double precision
	${PROJECT_SOURCE_DIR}/blas/d_blas1_lib4.c
	${PROJECT_SOURCE_DIR}/blas/d_blas2_lib4.c
	${PROJECT_SOURCE_DIR}/blas/d_blas3_lib4.c
	${PROJECT_SOURCE_DIR}/blas/d_blas3_diag_lib4.c
	${PROJECT_SOURCE_DIR}/blas/d_lapack_lib4.c
	# single precision
	${PROJECT_SOURCE_DIR}/blas/s_blas2_lib4.c
	${PROJECT_SOURCE_DIR}/blas/s_blas3_lib4.c
	${PROJECT_SOURCE_DIR}/blas/s_lapack_lib4.c
	)

set(BLASFEO_SRC ${BLASFEO_AUXILIARY_C99_SRC} ${BLASFEO_KERNELS_SRC}
	${BLASFEO_BLAS_SRC})

# build variables
set(MACRO_LEVEL 0)

set(CMAKE_C_FLAGS "${CMAKE_FLAGS} -DLA_HIGH_PERFORMANCE	-DTARGET_GENERIC -DMACRO_LEVEL -DOS_LINUX")

# add library
add_library(blasfeo SHARED ${BLASFEO_SRC})
