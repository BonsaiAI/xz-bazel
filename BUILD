licenses(["notice"])

config_setting(
    name = "windows",
    values = {"cpu": "x64_windows"},
)

config_setting(
    name = "macos",
    values = {"cpu": "darwin"},
)

genrule(
    name = "config_h",
    srcs = select({
        ":windows": ["windows/config.h"],
        ":macos": ["macosx/config.h"],
        "//conditions:default": ["linux_x64/config.h"]
    }),
    outs = ["src/config.h"],
    cmd = "cp $< $@",
)

cc_library(
    name = "xz",
    srcs = glob(["src/*.c", "src/*.h"]) + [":config_h"],
    hdrs = glob(["include/**/*.h"]),
    defines = ["HAVE_CONFIG_H"],
    strip_include_prefix = "include",
    includes = ["src"],
    visibility = ["//visibility:public"]
)
