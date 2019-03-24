cmake_minimum_required(VERSION 3.10)

set(CMAKE_TOOLCHAIN_FILE Toolchain-arm-gcc.cmake)

# Allow assembler
enable_language(ASM)

project(cmsis-nn-example)

set(INCLUDE_DIRS
    CMSIS/Core/Include
    CMSIS/DSP/Include
    CMSIS/NN/Include
    external/stm32
    hw
    utils
)

set(CPP_SRCS
	CMSIS/NN/Examples/ARM/arm_nn_examples/cifar10/arm_nnexamples_cifar10.cpp
)

set(C_SRCS
	hw/core_init/core_init.c
	hw/gpio_f4/gpio_f4.c
	hw/startup/hardfault.c
    hw/startup/vectors.c
    utils/syscalls.c
    CMSIS/NN/Source/ActivationFunctions/arm_nn_activations_q15.c
    CMSIS/NN/Source/ActivationFunctions/arm_nn_activations_q7.c
    CMSIS/NN/Source/ActivationFunctions/arm_relu_q15.c
    CMSIS/NN/Source/ActivationFunctions/arm_relu_q7.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_1x1_HWC_q7_fast_nonsquare.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_HWC_q15_basic.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_HWC_q15_fast_nonsquare.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_HWC_q15_fast.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_HWC_q7_basic_nonsquare.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_HWC_q7_basic.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_HWC_q7_fast_nonsquare.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_HWC_q7_fast.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_convolve_HWC_q7_RGB.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_depthwise_separable_conv_HWC_q7_nonsquare.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_depthwise_separable_conv_HWC_q7.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_nn_mat_mult_kernel_q7_q15_reordered.c
    CMSIS/NN/Source/ConvolutionFunctions/arm_nn_mat_mult_kernel_q7_q15.c
    CMSIS/NN/Source/FullyConnectedFunctions/arm_fully_connected_mat_q7_vec_q15_opt.c
    CMSIS/NN/Source/FullyConnectedFunctions/arm_fully_connected_mat_q7_vec_q15.c
    CMSIS/NN/Source/FullyConnectedFunctions/arm_fully_connected_q15_opt.c
    CMSIS/NN/Source/FullyConnectedFunctions/arm_fully_connected_q15.c
    CMSIS/NN/Source/FullyConnectedFunctions/arm_fully_connected_q7_opt.c
    CMSIS/NN/Source/FullyConnectedFunctions/arm_fully_connected_q7.c
    CMSIS/NN/Source/NNSupportFunctions/arm_nn_mult_q15.c
    CMSIS/NN/Source/NNSupportFunctions/arm_nn_mult_q7.c
    CMSIS/NN/Source/NNSupportFunctions/arm_nntables.c
    CMSIS/NN/Source/NNSupportFunctions/arm_q7_to_q15_no_shift.c
    CMSIS/NN/Source/NNSupportFunctions/arm_q7_to_q15_reordered_no_shift.c
    CMSIS/NN/Source/PoolingFunctions/arm_pool_q7_HWC.c
    CMSIS/NN/Source/SoftmaxFunctions/arm_softmax_q15.c
    CMSIS/NN/Source/SoftmaxFunctions/arm_softmax_q7.c
)

set(ASM_SRCS
    hw/startup/startup.S
)

set(GLOBAL_DEFINES
    -DSTM32F40_41xxx
)

set(LINKED_LIBS

)

link_directories(

)

include_directories(${INCLUDE_DIRS})
add_definitions(${GLOBAL_DEFINES})

include(compiler_flags.cmake)

# generate elf file
add_arm_executable(${CMAKE_PROJECT_NAME} ${CPP_SRCS} ${C_SRCS} ${ASM_SRCS})

arm_link_libraries(${CMAKE_PROJECT_NAME} ${LINKED_LIBS})
