#
#   This file is part of Magnum.
#
#   Copyright © 2010, 2011, 2012, 2013, 2014, 2015
#             Vladimír Vondruš <mosra@centrum.cz>
#
#   Permission is hereby granted, free of charge, to any person obtaining a
#   copy of this software and associated documentation files (the "Software"),
#   to deal in the Software without restriction, including without limitation
#   the rights to use, copy, modify, merge, publish, distribute, sublicense,
#   and/or sell copies of the Software, and to permit persons to whom the
#   Software is furnished to do so, subject to the following conditions:
#
#   The above copyright notice and this permission notice shall be included
#   in all copies or substantial portions of the Software.
#
#   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#   IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#   FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL
#   THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#   LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
#   FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
#   DEALINGS IN THE SOFTWARE.
#

corrade_add_test(AbstractImageTest AbstractImageTest.cpp LIBRARIES Magnum)
corrade_add_test(AbstractShaderProgramTest AbstractShaderProgramTest.cpp LIBRARIES Magnum)
corrade_add_test(ArrayTest ArrayTest.cpp)
corrade_add_test(ColorTest ColorTest.cpp LIBRARIES MagnumMathTestLib)
corrade_add_test(ContextTest ContextTest.cpp LIBRARIES Magnum)
corrade_add_test(DebugOutputTest DebugOutputTest.cpp LIBRARIES Magnum)
corrade_add_test(DefaultFramebufferTest DefaultFramebufferTest.cpp LIBRARIES Magnum)
corrade_add_test(FramebufferTest FramebufferTest.cpp LIBRARIES Magnum)
corrade_add_test(ImageTest ImageTest.cpp LIBRARIES Magnum)
corrade_add_test(ImageReferenceTest ImageReferenceTest.cpp LIBRARIES Magnum)
corrade_add_test(MeshTest MeshTest.cpp LIBRARIES Magnum)
corrade_add_test(RendererTest RendererTest.cpp LIBRARIES Magnum)
corrade_add_test(ResourceManagerTest ResourceManagerTest.cpp LIBRARIES Magnum)
corrade_add_test(SamplerTest SamplerTest.cpp LIBRARIES Magnum)
corrade_add_test(ShaderTest ShaderTest.cpp LIBRARIES Magnum)
corrade_add_test(VersionTest VersionTest.cpp LIBRARIES Magnum)

if(BUILD_GL_TESTS)
    corrade_add_test(AbstractObjectGLTest AbstractObjectGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(AbstractQueryGLTest AbstractQueryGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(AbstractTextureGLTest AbstractTextureGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(BufferGLTest BufferGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(ContextGLTest ContextGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(CubeMapTextureGLTest CubeMapTextureGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(DebugOutputGLTest DebugOutputGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(FramebufferGLTest FramebufferGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(MeshGLTest MeshGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(RenderbufferGLTest RenderbufferGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(SampleQueryGLTest SampleQueryGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(TextureGLTest TextureGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    corrade_add_test(TimeQueryGLTest TimeQueryGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})

    corrade_add_resource(AbstractShaderProgramGLTest_RES AbstractShaderProgramGLTestFiles/resources.conf)
    corrade_add_test(AbstractShaderProgramGLTest
        AbstractShaderProgramGLTest.cpp
        ${AbstractShaderProgramGLTest_RES}
        LIBRARIES ${GL_TEST_LIBRARIES})

    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/configure.h.cmake
                   ${CMAKE_CURRENT_BINARY_DIR}/configure.h)
    include_directories(BEFORE ${CMAKE_CURRENT_BINARY_DIR})
    corrade_add_test(ShaderGLTest ShaderGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})

    if(NOT MAGNUM_TARGET_GLES2)
        corrade_add_test(BufferImageGLTest BufferImageGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
        corrade_add_test(MultisampleTextureGLTest MultisampleTextureGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
        corrade_add_test(PrimitiveQueryGLTest PrimitiveQueryGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
        corrade_add_test(TextureArrayGLTest TextureArrayGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
        corrade_add_test(TransformFeedbackGLTest TransformFeedbackGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    endif()

    if(NOT MAGNUM_TARGET_GLES)
        corrade_add_test(BufferTextureGLTest BufferTextureGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
        corrade_add_test(CubeMapTextureArrayGLTest CubeMapTextureArrayGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
        corrade_add_test(RectangleTextureGLTest RectangleTextureGLTest.cpp LIBRARIES ${GL_TEST_LIBRARIES})
    endif()
endif()

set_target_properties(ResourceManagerTest PROPERTIES COMPILE_FLAGS -DCORRADE_GRACEFUL_ASSERT)

# Install bootstrap header for GL tests to be used in dependent projects
install(FILES AbstractOpenGLTester.h DESTINATION ${MAGNUM_INCLUDE_INSTALL_DIR}/Test)
