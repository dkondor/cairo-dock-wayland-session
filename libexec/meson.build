bins = [
  'cairo-dock-wayfire-session',
  'cd-session-setup-wayfire-config.py',
]

configure_file(configuration: conf_data, input: 'cairo-dock-wayfire-session.in',
	output: '@BASENAME@', install_dir: 'libexec')
# need to use the cmake format since we have literal strings in the format of "@VALUE@"
configure_file(configuration: conf_data, input: 'cd-session-setup-wayfire-config.py.in',
	output: '@BASENAME@', install_dir: 'libexec', format: 'cmake')
