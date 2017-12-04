project('libpng', 'c', version : '1.6.17', license : 'libpng')

cc = meson.get_compiler('c')

if cc.get_define('__ANDROID__') != ''
zdep = declare_dependency(link_args: '-lz')
else
zdep = dependency('zlib', fallback : ['zlib', 'zlib_dep'])
endif

m_dep = cc.find_library('m', required : false)

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


libpng = library('png',
  src,
  dependencies : [zdep, m_dep],
)

incdir = include_directories('.')

pngtest = executable('pngtest', 'pngtest.c',
  link_with : libpng)

test('pngtest', pngtest,
  args : '@0@/pngtest.png'.format(meson.current_source_dir()))

png_dep = declare_dependency(link_with : libpng,
  include_directories : incdir)
