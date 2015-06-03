project('libpng', 'c')

zdep = dependency('zlib', required : false)

if zdep.found()
  zinc = []
  zlib = []
else
  zproj = subproject('zlib')
  zinc = [zproj.get_variable('incdir')]
  zlib = [zproj.get_variable('zlib')]
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


if get_option('shared_lib')
  libtype = 'shared_library'
else
  libtype = 'static_library'
endif

libpng = build_target('png',
  src,
  link_with : zlib,
  include_directories : zinc,
  dependencies : zdep,
  target_type : libtype,
)

incdir = include_directories('.')

pngtest = executable('pngtest', 'pngtest.c',
  link_with : libpng)

test('pngtest', pngtest,
  args : '@0@/pngtest.png'.format(meson.current_source_dir()))
