project('inytag', 'cpp', version : '1.0')
gettext_version = meson.project_version()
gettext_name = meson.project_name()
pkg = import('pkgconfig')

dependencies = [
    dependency('taglib'),
    dependency('gdk-pixbuf-2.0'),
    dependency('glib-2.0'),
]


subdir('source')
subdir('vapi')
