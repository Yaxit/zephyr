if(CONFIG_KISSFFT)

set(KISSFFT_DIR ${ZEPHYR_CURRENT_MODULE_DIR})

zephyr_library()

zephyr_library_compile_options(-Ofast)
zephyr_library_compile_definitions(KISSFFT_USE_ALLOCA=ON)
zephyr_include_directories(${KISSFFT_DIR})
zephyr_library_include_directories(${KISSFFT_DIR})

zephyr_library_sources(
    ${KISSFFT_DIR}/kfc.c
    ${KISSFFT_DIR}/kiss_fft.c
    ${KISSFFT_DIR}/kiss_fftnd.c
    ${KISSFFT_DIR}/kiss_fftndr.c
    ${KISSFFT_DIR}/kiss_fftr.c
)

endif()
