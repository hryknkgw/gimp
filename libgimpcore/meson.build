rootGimpCoreInclude = include_directories('.')

subdir('core')
subdir('file')
subdir('file-data')
subdir('gegl')
subdir('operations')
subdir('paint')
subdir('pdb')
subdir('plug-in')
subdir('text')
subdir('vectors')
subdir('xcf')


app_debug_files = files(
  'gimp-debug.c',
  'gimp-log.c',
)


if platform_windows
  # for GimpDashboard and GimpBacktrace
  psapi_cflags = [ '-DPSAPI_VERSION=1' ]
  link_args = [ '-lpsapi' ]

else
  psapi_cflags = [ ]
  link_args = []
endif

if platform_osx
  link_args += osx_ldflags
endif

libapp_dep = declare_dependency(
  dependencies: [
    cairo,
    dbghelp,
    drmingw,
    gegl,
    gexiv2,
    gio,
    gio_specific,
    gtk3,
    lcms,
    libbacktrace,
    pangocairo,
    pangoft2,
    rpc,
  ],
  link_with: [
    libappcore,
    libappfile,
    libappfiledata,
    libappgegl,
    libappinternalprocs,
    libapplayermodes,
    libapplayermodeslegacy,
    libappoperations,
    libapppaint,
    libapppdb,
    libappplugin,
    libapptext,
    libappvectors,
    libappxcf,
  ],
  include_directories: [
    rootInclude,
    rootGimpCoreInclude,
  ],
  compile_args: psapi_cflags,
  link_args: link_args,
)


# Those subdirs need to link against the first ones
subdir('config')



libgimpcore = library('gimpcore-' + gimp_app_version,
  app_debug_files,
  include_directories: [ rootInclude, rootGimpCoreInclude, ],
  c_args: [ '-DG_LOG_DOMAIN="Gimp"', '-DGIMP_APP_GLUE_COMPILATION', ],
  dependencies: [
    gegl,
    libbacktrace,
  ],
  link_whole: [
    libappconfig,
    libappcore,
    libappfile,
    libappfiledata,
    libappgegl,
    libappinternalprocs,
    libapplayermodes,
    libapplayermodeslegacy,
    libappoperations,
    libapppaint,
    libapppdb,
    libappplugin,
    libapptext,
    libappvectors,
    libappxcf,
  ],
  link_with: [
    libgimpbase,
    libgimpcolor,
    libgimpconfig,
    libgimpmath,
    libgimpmodule,
    libgimpthumb,
  ],
#  vs_module_defs: 'gimpcore.def',
  install: true,
  version: so_version,
)
