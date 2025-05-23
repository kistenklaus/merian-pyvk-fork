project('fmt', 'cpp', version: '10.1.1', license: 'BSD', default_options: ['cpp_std=c++20'])

fmt_private_cpp_args = []
if get_option('default_library') == 'shared'
  fmt_private_cpp_args += ['-DFMT_LIB_EXPORT']
endif

fmt_lib = library(
  'fmt',
  'src/format.cc',
  'src/os.cc',
  cpp_args: fmt_private_cpp_args,
  include_directories: 'include',
  install: false,
)

install_subdir('include',
  strip_directory: true,
  install_dir: get_option('includedir'),
)

fmt_dep = declare_dependency(
  include_directories: 'include',
  link_with: fmt_lib,
)

if meson.version().version_compare('>=0.54.0')
  meson.override_dependency('fmt', fmt_dep)
endif

fmt_header_only_dep = declare_dependency(
  include_directories: 'include',
  compile_args: '-DFMT_HEADER_ONLY',
)

pkg_mod = import('pkgconfig')
pkg_mod.generate(fmt_lib,
  name: 'fmt',
  filebase: 'fmt',
)
