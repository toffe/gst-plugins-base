orcsrc = 'gstvideotestsrcorc'
if have_orcc
  orc_h = custom_target(orcsrc + '.h',
    input : orcsrc + '.orc',
    output : orcsrc + '.h',
    command : orcc_args + ['--header', '-o', '@OUTPUT@', '@INPUT@'])
  orc_c = custom_target(orcsrc + '.c',
    input : orcsrc + '.orc',
    output : orcsrc + '.c',
    command : orcc_args + ['--implementation', '-o', '@OUTPUT@', '@INPUT@'])
else
  orc_h = configure_file(input : orcsrc + '-dist.h',
    output : orcsrc + '.h',
    configuration : configuration_data())
  orc_c = configure_file(input : orcsrc + '-dist.c',
    output : orcsrc + '.c',
    configuration : configuration_data())
endif

gstvideotestsrc = library('gstvideotestsrc',
  'gstvideotestsrc.c', 'videotestsrc.c', orc_c, orc_h,
  c_args : gst_plugins_base_args,
  include_directories: [configinc, libsinc],
  dependencies : glib_deps + [video_dep, gst_dep, gst_base_dep, libm],
  install : true,
  install_dir : plugins_install_dir,
)
