sources = files([
  'sample_source.cpp'
])

src = include_directories('.')

sources += configure_file(output : 'config.cpp', input : 'config.cpp.in',
  configuration : {
  'group' : group,
  'project' : meson.project_name(),
  'version' : meson.project_version(),
  'build' : run_command('git', 'describe').stdout().strip(),
  'maintainer' : maintainer,
})

static_lib = static_library(meson.project_name(), sources, include_directories : includes, install: true, dependencies: module_deps)
shared_lib = shared_library(meson.project_name(), sources, include_directories : includes, install: true, dependencies: module_deps)
