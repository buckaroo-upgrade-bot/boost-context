load('//:subdir_glob.bzl', 'subdir_glob')
load('//:buckaroo_macros.bzl', 'buckaroo_deps')

macos_srcs = glob([
  'src/posix/**/*.cpp',
]) + [
  'src/asm/jump_x86_64_sysv_macho_gas.S',
  'src/asm/make_x86_64_sysv_macho_gas.S',
  'src/asm/ontop_x86_64_sysv_macho_gas.S',
]

linux_srcs = glob([
  'src/posix/**/*.cpp',
]) + [
  'src/asm/jump_x86_64_sysv_elf_gas.S',
  'src/asm/make_x86_64_sysv_elf_gas.S',
  'src/asm/ontop_x86_64_sysv_elf_gas.S',
]

cxx_library(
  name = 'context',
  header_namespace = 'boost/context',
  exported_headers = subdir_glob([
    ('include/boost/context', '**/*.hpp'),
    ('include/boost/context', '**/*.ipp'),
  ]),
  srcs = glob([
    'src/*.cpp',
    'src/asm/**/*.cpp',
  ],
  exclude = [
    'src/unsupported.cpp',
    'src/untested.cpp',
  ]),
  platform_srcs = [
    ('default', linux_srcs),
    ('^macos.*', macos_srcs),
    ('^linux.*', linux_srcs),
    ('^windows.*', glob([ 'src/windows/**/*.cpp' ])),
  ],
  deps = buckaroo_deps(),
  visibility = [
    'PUBLIC',
  ],
)
