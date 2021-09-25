headers = files(
  'inytag.h'
 )

install_headers(headers, subdir : gettext_name)

sources = files(
  'inytag.cc'
)

inytag_files = [
    sources,
    headers,
]

cdata = configuration_data()
zlib_dep = dependency('zlib', required : false)
if not zlib_dep.found()
  zlib_dep = cc.find_library('z', required : false)
  if not zlib_dep.found() or not cc.has_header('zlib.h')
    zlib_dep = subproject('zlib').get_variable('zlib_dep')
  endif
endif
cdata.set('HAVE_ZLIB', true)

configure_file(output : 'config.h', configuration : cdata)

extra_args = []
cxx = meson.get_compiler('cpp')
if cxx.has_argument('-fvisibility=hidden')
    extra_args += ['-fvisibility=hidden']
endif
if cxx.has_argument('-fno-strict-aliasing')
    extra_args += ['-fno-strict-aliasing']
endif

libinytag = static_library(
    gettext_name,
    inytag_files,
    c_args : ['-DHAVE_CONFIG_H'],
    cpp_args : ['-DHAVE_CONFIG_H'] + extra_args,
    dependencies : [
        dependencies
    ],
    install: true,
)

pkg.generate(
    libraries : libinytag,
    subdirs: gettext_name,
    name : gettext_name,
    requires : dependencies,
    description : 'Taglib For Vala',
    version : gettext_version,
    filebase : gettext_name
)
