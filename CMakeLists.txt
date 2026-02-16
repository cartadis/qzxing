cmake_minimum_required(VERSION 3.16)

# --------------------------------------------------
# Project definition
# --------------------------------------------------
project(QZXing LANGUAGES CXX)

# -----------------------------
# Options
# -----------------------------
option(ENABLE_DECODER_1D_BARCODES   "Enable 1D barcode decoder" ON)
option(ENABLE_DECODER_QR_CODE       "Enable QR code decoder" ON)
option(ENABLE_DECODER_DATA_MATRIX   "Enable Data Matrix decoder" ON)
option(ENABLE_DECODER_AZTEC         "Enable Aztec decoder" ON)
option(ENABLE_DECODER_PDF17         "Enable PDF417 decoder" ON)
option(ENABLE_ENCODER_QR_CODE       "Enable QR code encoder" ON)
option(ENABLE_QML_SUPPORT           "Enable QML support" ON)
option(ENABLE_MULTIMEDIA_SUPPORT    "Enable Multimedia support" ON)

# -----------------------------
# C++ standard
# -----------------------------
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# -----------------------------
# Qt
# -----------------------------
find_package(Qt5 REQUIRED COMPONENTS Core Gui Widgets)
if(ENABLE_QML_SUPPORT)
    find_package(Qt5 REQUIRED COMPONENTS Qml)
endif()
if(ENABLE_MULTIMEDIA_SUPPORT)
    find_package(Qt5 REQUIRED COMPONENTS Multimedia)
endif()

# -----------------------------
# Sources files
# -----------------------------
set(QZXING_SOURCES
        src/CameraImageWrapper.cpp
        src/QZXing.cpp
        src/ImageHandler.cpp
        src/zxing/zxing/ResultIO.cpp
        src/zxing/zxing/InvertedLuminanceSource.cpp
        src/zxing/zxing/ChecksumException.cpp
        src/zxing/zxing/ResultPointCallback.cpp
        src/zxing/zxing/ResultPoint.cpp
        src/zxing/zxing/Result.cpp
        src/zxing/zxing/ResultMetadata.cpp
        src/zxing/zxing/Reader.cpp
        src/zxing/zxing/MultiFormatReader.cpp
        src/zxing/zxing/LuminanceSource.cpp
        src/zxing/zxing/FormatException.cpp
        src/zxing/zxing/Exception.cpp
        src/zxing/zxing/DecodeHints.cpp
        src/zxing/zxing/BinaryBitmap.cpp
        src/zxing/zxing/Binarizer.cpp
        src/zxing/zxing/BarcodeFormat.cpp
        src/zxing/zxing/ReaderException.cpp
        src/zxing/zxing/IllegalStateException.cpp
        src/zxing/zxing/NotFoundException.cpp
        src/zxing/zxing/WriterException.cpp
        src/zxing/zxing/common/StringUtils.cpp
        src/zxing/zxing/common/Str.cpp
        src/zxing/zxing/common/PerspectiveTransform.cpp
        src/zxing/zxing/common/IllegalArgumentException.cpp
        src/zxing/zxing/common/HybridBinarizer.cpp
        src/zxing/zxing/common/GridSampler.cpp
        src/zxing/zxing/common/GreyscaleRotatedLuminanceSource.cpp
        src/zxing/zxing/common/GreyscaleLuminanceSource.cpp
        src/zxing/zxing/common/GlobalHistogramBinarizer.cpp
        src/zxing/zxing/common/DetectorResult.cpp
        src/zxing/zxing/common/DecoderResult.cpp
        src/zxing/zxing/common/CharacterSetECI.cpp
        src/zxing/zxing/common/BitSource.cpp
        src/zxing/zxing/common/BitMatrix.cpp
        src/zxing/zxing/common/BitArray.cpp
        src/zxing/zxing/common/BitArrayIO.cpp
        src/zxing/zxing/common/detector/WhiteRectangleDetector.cpp
        src/zxing/zxing/common/detector/MonochromeRectangleDetector.cpp
        src/zxing/zxing/common/reedsolomon/ReedSolomonException.cpp
        src/zxing/zxing/common/reedsolomon/ReedSolomonDecoder.cpp
        src/zxing/zxing/common/reedsolomon/ReedSolomonEncoder.cpp
        src/zxing/zxing/common/reedsolomon/GenericGFPoly.cpp
        src/zxing/zxing/common/reedsolomon/GenericGF.cpp
        src/zxing/zxing/multi/MultipleBarcodeReader.cpp
        src/zxing/zxing/multi/GenericMultipleBarcodeReader.cpp
        src/zxing/zxing/multi/ByQuadrantReader.cpp
        src/zxing/bigint/BigUnsignedInABase.cc
        src/zxing/bigint/BigUnsigned.cc
        src/zxing/bigint/BigIntegerUtils.cc
        src/zxing/bigint/BigIntegerAlgorithms.cc
        src/zxing/bigint/BigInteger.cc
    )

set(QZXING_HEADERS
        src/QZXing_global.h
        src/CameraImageWrapper.h
        src/ImageHandler.h
        src/QZXing.h
        src/zxing/zxing/ZXing.h
        src/zxing/zxing/IllegalStateException.h
        src/zxing/zxing/InvertedLuminanceSource.h
        src/zxing/zxing/ChecksumException.h
        src/zxing/zxing/ResultPointCallback.h
        src/zxing/zxing/ResultPoint.h
        src/zxing/zxing/Result.h
        src/zxing/zxing/ResultMetadata.h
        src/zxing/zxing/ReaderException.h
        src/zxing/zxing/Reader.h
        src/zxing/zxing/NotFoundException.h
        src/zxing/zxing/MultiFormatReader.h
        src/zxing/zxing/LuminanceSource.h
        src/zxing/zxing/FormatException.h
        src/zxing/zxing/Exception.h
        src/zxing/zxing/DecodeHints.h
        src/zxing/zxing/BinaryBitmap.h
        src/zxing/zxing/Binarizer.h
        src/zxing/zxing/BarcodeFormat.h
        src/zxing/zxing/common/StringUtils.h
        src/zxing/zxing/common/Str.h
        src/zxing/zxing/common/Point.h
        src/zxing/zxing/common/PerspectiveTransform.h
        src/zxing/zxing/common/IllegalArgumentException.h
        src/zxing/zxing/common/HybridBinarizer.h
        src/zxing/zxing/common/GridSampler.h
        src/zxing/zxing/common/GreyscaleRotatedLuminanceSource.h
        src/zxing/zxing/common/GreyscaleLuminanceSource.h
        src/zxing/zxing/common/GlobalHistogramBinarizer.h
        src/zxing/zxing/common/DetectorResult.h
        src/zxing/zxing/common/DecoderResult.h
        src/zxing/zxing/common/CharacterSetECI.h
        src/zxing/zxing/common/BitSource.h
        src/zxing/zxing/common/BitMatrix.h
        src/zxing/zxing/common/BitArray.h
        src/zxing/zxing/common/detector/MathUtils.h
        src/zxing/zxing/common/detector/JavaMath.h
        src/zxing/zxing/common/detector/WhiteRectangleDetector.h
        src/zxing/zxing/common/detector/MonochromeRectangleDetector.h
        src/zxing/zxing/common/reedsolomon/ReedSolomonException.h
        src/zxing/zxing/common/reedsolomon/ReedSolomonDecoder.h
        src/zxing/zxing/common/reedsolomon/ReedSolomonEncoder.h
        src/zxing/zxing/common/reedsolomon/GenericGFPoly.h
        src/zxing/zxing/common/reedsolomon/GenericGF.h
        src/zxing/zxing/common/ByteArray.h
        src/zxing/zxing/multi/MultipleBarcodeReader.h
        src/zxing/zxing/multi/GenericMultipleBarcodeReader.h
        src/zxing/zxing/multi/ByQuadrantReader.h
        src/zxing/bigint/NumberlikeArray.hh
        src/zxing/bigint/BigUnsignedInABase.hh
        src/zxing/bigint/BigUnsigned.hh
        src/zxing/bigint/BigIntegerUtils.hh
        src/zxing/bigint/BigIntegerLibrary.hh
        src/zxing/bigint/BigIntegerAlgorithms.hh
        src/zxing/bigint/BigInteger.hh
        src/zxing/zxing/WriterException.h
        src/zxing/zxing/common/Types.h
    )

# -----------------------------
# Conditional sources based on options
# -----------------------------
if(ENABLE_DECODER_1D_BARCODES)
    file(GLOB_RECURSE QZXING_1D_SOURCES src/zxing/zxing/oned/*.cpp src/zxing/zxing/oned/rss/*.cpp src/zxing/zxing/oned/rss/expanded/decoders/*.cpp)
    file(GLOB_RECURSE QZXING_1D_HEADERS src/zxing/zxing/oned/*.h src/zxing/zxing/oned/rss/*.h src/zxing/zxing/oned/rss/expanded/decoders/*.h)
    list(APPEND QZXING_SOURCES ${QZXING_1D_SOURCES})
    list(APPEND QZXING_HEADERS ${QZXING_1D_HEADERS})
endif()

if(ENABLE_DECODER_QR_CODE OR ENABLE_ENCODER_QR_CODE)
    file(GLOB_RECURSE QZXING_QR_SOURCES src/zxing/zxing/qrcode/*.cpp src/zxing/zxing/multi/qrcode/*.cpp)
    file(GLOB_RECURSE QZXING_QR_HEADERS src/zxing/zxing/qrcode/*.h src/zxing/zxing/multi/qrcode/*.h)
    list(APPEND QZXING_SOURCES ${QZXING_QR_SOURCES})
    list(APPEND QZXING_HEADERS ${QZXING_QR_HEADERS})
endif()

if(ENABLE_DECODER_DATA_MATRIX)
    file(GLOB_RECURSE QZXING_DATAMATRIX_SOURCES src/zxing/zxing/datamatrix/*.cpp)
    file(GLOB_RECURSE QZXING_DATAMATRIX_HEADERS src/zxing/zxing/datamatrix/*.h)
    list(APPEND QZXING_SOURCES ${QZXING_DATAMATRIX_SOURCES})
    list(APPEND QZXING_HEADERS ${QZXING_DATAMATRIX_HEADERS})
endif()

if(ENABLE_DECODER_AZTEC)
    file(GLOB_RECURSE QZXING_AZTEC_SOURCES src/zxing/zxing/aztec/*.cpp)
    file(GLOB_RECURSE QZXING_AZTEC_HEADERS src/zxing/zxing/aztec/*.h)
    list(APPEND QZXING_SOURCES ${QZXING_AZTEC_SOURCES})
    list(APPEND QZXING_HEADERS ${QZXING_AZTEC_HEADERS})
endif()

if(ENABLE_DECODER_PDF17)
    file(GLOB_RECURSE QZXING_PDF417_SOURCES src/zxing/zxing/pdf417/*.cpp)
    file(GLOB_RECURSE QZXING_PDF417_HEADERS src/zxing/zxing/pdf417/*.h)
    list(APPEND QZXING_SOURCES ${QZXING_PDF417_SOURCES})
    list(APPEND QZXING_HEADERS ${QZXING_PDF417_HEADERS})
endif()

if(ENABLE_MULTIMEDIA_SUPPORT)
    list(APPEND QZXING_SOURCES src/QZXingFilter.cpp)
    list(APPEND QZXING_HEADERS src/QZXingFilter.h)
endif()

if(ENABLE_QML_SUPPORT)
    list(APPEND QZXING_SOURCES src/QZXingImageProvider.cpp)
    list(APPEND QZXING_HEADERS src/QZXingImageProvider.h)
endif()


add_library(QZXing SHARED
    ${QZXING_SOURCES}
    ${QZXING_HEADERS}
)

# --------------------------------------------------
# Include directories
# --------------------------------------------------
target_include_directories(QZXing
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/src
        ${CMAKE_CURRENT_SOURCE_DIR}/src/zxing
)

# --------------------------------------------------
# Link Qt libraries (this adds the include dirs)
# --------------------------------------------------
target_link_libraries(QZXing
    PUBLIC
        Qt5::Core
        Qt5::Gui
        Qt5::Widgets
)

if(ENABLE_QML_SUPPORT)
    target_link_libraries(QZXing
        PUBLIC
            Qt5::Qml
            Qt5::Quick
    )
endif()

if(ENABLE_MULTIMEDIA_SUPPORT)
    target_link_libraries(QZXing
        PUBLIC
            Qt5::Multimedia
    )
endif()

# -----------------------------
# Compile definitions
# -----------------------------
target_compile_definitions(QZXing
    PUBLIC QZXING_LIBRARY
)

if(ENABLE_DECODER_1D_BARCODES)
    target_compile_definitions(QZXing PUBLIC ENABLE_DECODER_1D_BARCODES)
endif()
if(ENABLE_DECODER_QR_CODE)
    target_compile_definitions(QZXing PUBLIC ENABLE_DECODER_QR_CODE)
endif()
if(ENABLE_DECODER_DATA_MATRIX)
    target_compile_definitions(QZXing PUBLIC ENABLE_DECODER_DATA_MATRIX)
endif()
if(ENABLE_DECODER_AZTEC)
    target_compile_definitions(QZXing PUBLIC ENABLE_DECODER_AZTEC)
endif()
if(ENABLE_DECODER_PDF17)
    target_compile_definitions(QZXing PUBLIC ENABLE_DECODER_PDF17)
endif()
if(ENABLE_ENCODER_QR_CODE)
    target_compile_definitions(QZXing PUBLIC ENABLE_ENCODER_QR_CODE ENABLE_ENCODER_GENERIC)
endif()
if(ENABLE_QML_SUPPORT)
    target_compile_definitions(QZXing PUBLIC QZXING_QML)
endif()
if(ENABLE_MULTIMEDIA_SUPPORT)
    target_compile_definitions(QZXing PUBLIC QZXING_MULTIMEDIA)
endif()


# --------------------------------------------------
# Installation

# If INSTALL_LIB_DIR is not defined by the parent project or toolchain,
# fall back to the standard system library directory.
# This makes the library usable both in standalone builds
# and when included in a larger cross-compiled project.
# --------------------------------------------------
if(NOT DEFINED INSTALL_LIB_DIR)
    set(INSTALL_LIB_DIR lib)
endif()

install(TARGETS QZXing
    LIBRARY DESTINATION ${INSTALL_LIB_DIR}
)
