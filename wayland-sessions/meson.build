desktop_files = [
  'cairo-dock-wayfire.desktop'
]

foreach f : desktop_files
	configure_file(configuration: conf_data, input: f + '.in',
		output: '@BASENAME@', install_dir: 'share/wayland-sessions')
endforeach
