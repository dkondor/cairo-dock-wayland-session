project('cairo-dock-wayland-session',
  version: '1.0',
  meson_version: '>=0.61'
)

datadir = get_option('prefix') / get_option('datadir') / 'cairo-dock-wayland-session'
conf_data = configuration_data()
conf_data.set('libexec', get_option('prefix') / 'libexec')
conf_data.set('datadir', datadir)

subdir('libexec')
subdir('systemd')
subdir('wayland-sessions')
subdir('data')
