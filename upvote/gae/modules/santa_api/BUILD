load(
    "//upvote:builddefs.bzl",
    "py_appengine_library",
    "py_appengine_binary",
    "upvote_appengine_test",
)

package(default_visibility = ["//upvote"])

# AppEngine Libraries
# ==============================================================================

py_appengine_library(
    name = "all",
    deps = [
        ":sync",
    ],
)

py_appengine_library(
    name = "sync",
    srcs = ["sync.py"],
    deps = [
        ":auth",
        ":constants",
        ":monitoring",
        "//upvote/gae/datastore:utils",
        "//upvote/gae/datastore/models:base",
        "//upvote/gae/datastore/models:bigquery",
        "//upvote/gae/datastore/models:santa",
        "//upvote/gae/shared/binary_health:metrics",
        "//upvote/gae/shared/common:big_red",
        "//upvote/gae/shared/common:handlers",
        "//upvote/gae/shared/common:query_utils",
        "//upvote/gae/shared/common:settings",
        "//upvote/gae/shared/common:taskqueue_utils",
        "//upvote/gae/shared/common:user_map",
        "//upvote/gae/shared/common:utils",
        "//upvote/gae/shared/common:xsrf_utils",
        "//upvote/shared:constants",
    ],
)

py_appengine_library(
    name = "constants",
    srcs = ["constants.py"],
    deps = [
        "//upvote/shared:constants",
    ],
)

py_appengine_library(
    name = "monitoring",
    srcs = ["monitoring.py"],
    deps = [
        "//upvote/gae/shared/common:monitoring",
        "//upvote/monitoring:metrics",
    ],
)

py_appengine_library(
    name = "santa_api_library",
    srcs = [
        "main.py",
    ],
    data = [
        "//upvote/gae:santa_api.yaml",
    ],
    deps = [
        ":auth",
        ":monitoring",
        ":sync",
        "//upvote/gae/shared/common:handlers",
        "//upvote/shared:constants",
    ],
)

py_appengine_library(
    name = "auth",
    srcs = ["auth.py"],
)

py_appengine_binary(
    name = "santa_api_binary",
    srcs = ["main.py"],
    configs = [
        "//upvote/gae:appengine_config.py",
        "//upvote/gae:santa_api.yaml",
    ],
    deps = [
        ":santa_api_library",
        "//upvote/gae/shared/common:utils",
    ],
)

# AppEngine Unit Tests
# ==============================================================================

upvote_appengine_test(
    name = "sync_test",
    size = "small",
    srcs = ["sync_test.py"],
    deps = [
        ":sync",
        "//external:mock",
        "//external:webtest",
        "//upvote/gae/datastore:test_utils",
        "//upvote/gae/datastore/models:santa",
        "//upvote/gae/shared/common:basetest",
        "//upvote/gae/shared/common:handlers",
        "//upvote/gae/shared/common:settings_utils",
        "//upvote/shared:constants",
    ],
)

upvote_appengine_test(
    name = "monitoring_test",
    size = "small",
    srcs = ["monitoring_test.py"],
    deps = [
        ":monitoring",
        "//common/testing:basetest",
    ],
)

upvote_appengine_test(
    name = "main_test",
    size = "small",
    srcs = ["main_test.py"],
    deps = [
        ":santa_api_library",
        "//upvote/gae/shared/common:basetest",
    ],
)
