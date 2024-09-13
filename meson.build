#
# Copyright (C) 2019 Purism SPC
# Copyright (C) 2020 Arnaud Ferraris <arnaud.ferraris@gmail.com>
#
# SPDX-License-Identifier: GPL-3.0-or-later
#

project (
  'callaudiod',
  'c',
  version : '0.1.9',
  license : 'LGPLv3+',
  meson_version : '>= 0.50.0',
  default_options :
    [
      'warning_level=1',
      'buildtype=debugoptimized',
      'c_std=gnu11'
    ],
)

cc = meson.get_compiler('c')

cc = meson.get_compiler('c')

global_c_args = []
test_c_args = [
  '-Wcast-align',
  '-Wdate-time',
  '-Wdeclaration-after-statement',
  ['-Werror=format-security', '-Werror=format=2'],
  '-Wendif-labels',
  '-Werror=incompatible-pointer-types',
  '-Werror=missing-declarations',
  '-Werror=overflow',
  '-Werror=return-type',
  '-Werror=shift-count-overflow',
  '-Werror=shift-overflow=2',
  '-Werror=implicit-fallthrough=3',
  '-Wfloat-equal',
  '-Wformat-nonliteral',
  '-Wformat-security',
  '-Winit-self',
  '-Wmaybe-uninitialized',
  '-Wmissing-field-initializers',
  '-Wmissing-include-dirs',
  '-Wmissing-noreturn',
  '-Wnested-externs',
  '-Wno-missing-field-initializers',
  '-Wno-sign-compare',
  '-Wno-strict-aliasing',
  '-Wno-unused-parameter',
  '-Wold-style-definition',
  '-Wpointer-arith',
  '-Wredundant-decls',
  '-Wshadow',
  '-Wstrict-prototypes',
  '-Wswitch-default',
  '-Wswitch-enum',
  '-Wtype-limits',
  '-Wundef',
  '-Wunused-function',
]
foreach arg: test_c_args
  if cc.has_multi_arguments(arg)
    global_c_args += arg
  endif
endforeach
add_project_arguments(
  global_c_args,
  language: 'c'
)

app_name = meson.project_name()

prefix = get_option('prefix')
datadir = get_option('datadir')
sysconfdir = get_option('sysconfdir')
bindir = join_paths(prefix, get_option('bindir'))
libdir = join_paths(prefix, get_option('libdir'))
ifacedir = join_paths(prefix, join_paths(datadir, 'dbus-1', 'interfaces'))
servicedir = join_paths(prefix, join_paths(datadir, 'dbus-1', 'services'))

if datadir.startswith('/')
  full_datadir = datadir
else
  full_datadir = join_paths(prefix, datadir)
endif

if sysconfdir.startswith('/')
  full_sysconfdir = sysconfdir
else
  full_sysconfdir = join_paths(prefix, sysconfdir)
endif

apiversion = '0.1'
libname = 'libcallaudio-' + apiversion

config_data = configuration_data()
config_data.set_quoted('APP_DATA_NAME', app_name)
config_data.set_quoted('DATADIR', full_datadir)
config_data.set_quoted('SYSCONFDIR', full_sysconfdir)

config_h = configure_file (
    output: 'config.h',
    configuration: config_data
)

subdir('data')
subdir('libcallaudio')
subdir('src')
subdir('tools')
subdir('doc')
