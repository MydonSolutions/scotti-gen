project('scotti-gen', 'c',
  version: '0.0.1',
  default_options: [
    'c_std=c99',
    'buildtype=release',
    'b_ndebug=if-release'
  ]
)

add_project_arguments('-D_POSIX_C_SOURCE=199309L', language : 'c')

cc = meson.get_compiler('c')
m_dep = cc.find_library('m', required : true)

src_lst = []
inc_lst = [
	include_directories('include'),
]
dep_lst = [
  m_dep,
  dependency('hdf5'),
]

subdir('src')

lib_scottigen = library(
  'scotti-gen',
  src_lst,
  include_directories: inc_lst,
  dependencies: dep_lst,
  install: false,
)

lib_scottigen_dep = declare_dependency(
  include_directories: inc_lst,
  dependencies: dep_lst,
  link_with: lib_scottigen,
)

pkg = import('pkgconfig')
pkg.generate(
  lib_scottigen,
  libraries: dep_lst,
)

subdir('app')