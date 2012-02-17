envspooky = Environment(CPPPATH = ['deps/spookyhash/'], CPPFLAGS="-O2")
spooky = envspooky.Library('spooky', Glob("deps/spookyhash/*.cpp"))

envmurmur = Environment(CPPPATH = ['deps/murmurhash/'], CPPFLAGS="-O2")
murmur = envmurmur.Library('murmur', Glob("deps/murmurhash/*.cpp"))

envbloom = Environment(CCFLAGS = '-std=c99 -Wall -Werror -O2')
bloom = envbloom.Library('bloom', Glob("src/libbloom/*.c"))

envtest = Environment(CCFLAGS = '-std=c99 -Isrc/libbloom/')
envtest.Program('test_libbloom_runner', spooky + murmur + bloom +  Glob("tests/libbloom/*.c"), LIBS=["libcheck"])

envinih = Environment(CPATH = ['deps/inih/'], CFLAGS="-O2")
inih = envinih.Library('inih', Glob("deps/inih/*.c"))

envbloomd = Environment(CCFLAGS = '-std=c99 -Wall -Werror -O2 -Ideps/inih/')
objs = envbloomd.Object('src/config/config', 'src/bloomd/config.c')
bloomd = envbloomd.Program('bloomd', spooky + murmur + bloom + inih + objs + ["src/bloomd/bloomd.c"])

envtest2 = Environment(CCFLAGS = '-std=c99 -Isrc/bloomd/ -Ideps/inih/')
envtest2.Program('test_bloomd_runner', spooky + murmur + bloom + inih + objs + Glob("tests/bloomd/*.c"), LIBS=["libcheck"])

