# Copyright (c) 2023 Meta Platforms
# SPDX-License-Identifier: Apache-2.0

if(CONFIG_ESP_NN)

  set(ESP_NN_DIR ${ZEPHYR_CURRENT_MODULE_DIR})

  zephyr_library()

  zephyr_library_compile_options(-Ofast)

  zephyr_include_directories(${ESP_NN_DIR}/include)
  zephyr_library_include_directories(${ESP_NN_DIR}/include ${ESP_NN_DIR}/src/common)

  # todo: test this
  if(CONFIG_SOC_SERIES_ESP32S3)
    set(s3_srcs
        ${ESP_NN_DIR}src/common/esp_nn_common_functions_esp32s3.S
        ${ESP_NN_DIR}src/common/esp_nn_multiply_by_quantized_mult_esp32s3.S
        ${ESP_NN_DIR}src/common/esp_nn_multiply_by_quantized_mult_ver1_esp32s3.S
        ${ESP_NN_DIR}src/activation_functions/esp_nn_relu_s8_esp32s3.S
        ${ESP_NN_DIR}src/basic_math/esp_nn_add_s8_esp32s3.S
        ${ESP_NN_DIR}src/basic_math/esp_nn_mul_s8_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_conv_esp32s3.c
        ${ESP_NN_DIR}src/convolution/esp_nn_depthwise_conv_s8_esp32s3.c
        ${ESP_NN_DIR}src/convolution/esp_nn_conv_s16_mult8_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_conv_s8_mult8_1x1_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_conv_s16_mult4_1x1_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_conv_s8_filter_aligned_input_padded_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_depthwise_conv_s8_mult1_3x3_padded_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_depthwise_conv_s16_mult1_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_depthwise_conv_s16_mult1_3x3_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_depthwise_conv_s16_mult1_3x3_no_pad_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_depthwise_conv_s16_mult8_3x3_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_depthwise_conv_s16_mult4_esp32s3.S
        ${ESP_NN_DIR}src/convolution/esp_nn_depthwise_conv_s16_mult8_esp32s3.S
        ${ESP_NN_DIR}src/fully_connected/esp_nn_fully_connected_s8_esp32s3.S
        ${ESP_NN_DIR}src/pooling/esp_nn_max_pool_s8_esp32s3.S
        ${ESP_NN_DIR}src/pooling/esp_nn_avg_pool_s8_esp32s3.S)
        # todo: add compile options for this as well
  endif()

  zephyr_library_compile_options(-Wno-unused-function)
  zephyr_library_sources(
    ${ESP_NN_DIR}/src/activation_functions/esp_nn_relu_ansi.c
    ${ESP_NN_DIR}/src/basic_math/esp_nn_add_ansi.c
    ${ESP_NN_DIR}/src/basic_math/esp_nn_mul_ansi.c
    ${ESP_NN_DIR}/src/convolution/esp_nn_conv_ansi.c
    ${ESP_NN_DIR}/src/convolution/esp_nn_conv_opt.c
    ${ESP_NN_DIR}/src/convolution/esp_nn_depthwise_conv_ansi.c
    ${ESP_NN_DIR}/src/convolution/esp_nn_depthwise_conv_opt.c
    ${ESP_NN_DIR}/src/fully_connected/esp_nn_fully_connected_ansi.c
    ${ESP_NN_DIR}/src/softmax/esp_nn_softmax_ansi.c
    ${ESP_NN_DIR}/src/softmax/esp_nn_softmax_opt.c
    ${ESP_NN_DIR}/src/pooling/esp_nn_avg_pool_ansi.c
    ${ESP_NN_DIR}/src/pooling/esp_nn_max_pool_ansi.c
    ${s3_srcs})

endif()
