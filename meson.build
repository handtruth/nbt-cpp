project('cpp-meson', 'cpp',
  version : run_command('git', 'describe', '--abbrev=0', '--tags').stdout().strip(),
  default_options : ['warning_level=3',
                     'cpp_std=c++17'])

group = 'com.handtruth'
maintainer = 'someone <someone@handtruth.com>'

modules = [
]

######################################

module_deps = []

foreach module : modules
  module_deps += dependency(module, fallback : [module, 'dep'])
endforeach

subdir('include')
subdir('src')
subdir('test')

if get_option('link_type') == 'static'
  chosen_lib = static_lib
else
  chosen_lib = shared_lib
endif

dep = declare_dependency(link_with : chosen_lib, include_directories : includes)

cppcheck = custom_target(meson.project_name() + '_cppcheck_internal',
  output : meson.project_name() + '_cppcheck.log',
  input : sources + test_files,
  command : [
    'cppcheck',
    '--enable=all',
    '-I', meson.current_source_dir() / 'include',
    '-I', meson.current_source_dir() / 'src',
    '@INPUT@',
#   '--project=compile_commands.json',
    '--output-file=@OUTPUT@'
])

run_target('cppcheck', command : ['cat', cppcheck.full_path()], depends : cppcheck)
