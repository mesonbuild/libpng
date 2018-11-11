project('libpng', 'c', license : 'libpng')

cc = meson.get_compiler('c')

include = include_directories('.')

if cc.get_define('__ANDROID__') != ''
  zlib_dep = cc.find_library('z')
else
  zlib_dep = dependency('zlib', fallback : ['zlib', 'zlib_dep'])
endif

src = [
  'png.c',
  'pngerror.c',
  'pngget.c',
  'pngmem.c',
  'pngpread.c',
  'pngread.c',
  'pngrio.c',
  'pngrtran.c',
  'pngrutil.c',
  'pngset.c',
  'pngtrans.c',
  'pngwio.c',
  'pngwrite.c',
  'pngwtran.c',
  'pngwutil.c',
]
c_args = []

if host_machine.system() == 'windows'
  c_args += ['-DPNG_BUILD_DLL']
endif

if host_machine.cpu_family() == 'arm64' or cc.get_define('__ARM_NEON') != ''
  src += [
    'arm/arm_init.c',
    'arm/filter_neon_intrinsics.c',
    'arm/filter_neon.S',
  ]
  c_args += ['-DPNG_ARM_NEON_OPT=2']
endif

libpng_deps = [
        zlib_dep,
        cc.find_library('m', required : false),
]

libpng = library('png',
    src,
    dependencies : libpng_deps,
    c_args: c_args,
)

configure_file(
    configuration : configuration_data(),
    input : 'scripts/pnglibconf.h.prebuilt',
    output : 'pnglibconf.h',
)

png_dep = declare_dependency(
    include_directories : include,
    link_with : libpng,
    dependencies : libpng_deps,
)

png_test = executable('pngtest', 'pngtest.c', dependencies : png_dep)
test('pngtest', png_test, args : files('pngtest.png'))
