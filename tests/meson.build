check = dependency('check', required: false)
if check.found()
  test_dependencies = [
    declare_dependency(link_with: girara),
    check
  ]

  include_directories += [ include_directories('../girara') ]

  test_sources = [
    'tests.c',
    'test_config.c',
    'test_datastructures.c',
    'test_session.c',
    'test_setting.c',
    'test_template.c',
    'test_utils.c'
  ]

  xdg_test_helper = executable('xdg_test_helper', 'xdg_test_helper.c',
    dependencies: [ glib, declare_dependency(link_with: girara) ],
    include_directories: include_directories,
    c_args: defines + flags
  )

  tests = executable('tests', test_sources,
    dependencies: build_dependencies + test_dependencies,
    include_directories: include_directories,
    c_args: defines + flags
  )

  env = environment()
  env.set('XDG_TEST_HELPER_PATH', meson.current_build_dir())
  env.set('HOME', '/home/test')
  test('tests-with-home', tests, env: env)

  # Cannot unset environment variables.
  # env.unset('HOME')
  # test('tests-without-home', tests, env: env)
endif