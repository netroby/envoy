licenses(["notice"])  # Apache 2

load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_library",
    "envoy_package",
    "envoy_select_hot_restart",
)

envoy_package()

envoy_cc_library(
    name = "backtrace_lib",
    hdrs = ["backtrace.h"],
    external_deps = ["backward"],
    tags = ["backtrace"],
    deps = ["//source/common/common:logger_lib"],
)

envoy_cc_library(
    name = "configuration_lib",
    srcs = ["configuration_impl.cc"],
    hdrs = ["configuration_impl.h"],
    external_deps = [
        "envoy_bootstrap",
        "envoy_lds",
    ],
    deps = [
        ":lds_api_lib",
        "//include/envoy/http:filter_interface",
        "//include/envoy/network:connection_interface",
        "//include/envoy/network:filter_interface",
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/server:configuration_interface",
        "//include/envoy/server:filter_config_interface",
        "//include/envoy/server:instance_interface",
        "//include/envoy/ssl:context_manager_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:logger_lib",
        "//source/common/common:utility_lib",
        "//source/common/config:lds_json_lib",
        "//source/common/config:utility_lib",
        "//source/common/network:resolver_lib",
        "//source/common/network:utility_lib",
        "//source/common/protobuf:utility_lib",
        "//source/common/ratelimit:ratelimit_lib",
        "//source/common/tracing:http_tracer_lib",
    ],
)

envoy_cc_library(
    name = "connection_handler_lib",
    srcs = ["connection_handler_impl.cc"],
    hdrs = ["connection_handler_impl.h"],
    deps = [
        "//include/envoy/common:time_interface",
        "//include/envoy/event:deferred_deletable",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:timer_interface",
        "//include/envoy/network:connection_handler_interface",
        "//include/envoy/network:connection_interface",
        "//include/envoy/network:filter_interface",
        "//include/envoy/network:listen_socket_interface",
        "//include/envoy/network:listener_interface",
        "//include/envoy/stats:timespan",
        "//source/common/common:linked_object",
        "//source/common/common:non_copyable",
    ],
)

envoy_cc_library(
    name = "drain_manager_lib",
    srcs = ["drain_manager_impl.cc"],
    hdrs = ["drain_manager_impl.h"],
    deps = [
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:timer_interface",
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/server:drain_manager_interface",
        "//include/envoy/server:instance_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:logger_lib",
    ],
)

envoy_cc_library(
    name = "guarddog_lib",
    srcs = ["guarddog_impl.cc"],
    hdrs = ["guarddog_impl.h"],
    deps = [
        ":watchdog_lib",
        "//include/envoy/common:optional",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/server:configuration_interface",
        "//include/envoy/server:guarddog_interface",
        "//include/envoy/server:watchdog_interface",
        "//include/envoy/stats:stats_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:logger_lib",
        "//source/common/common:thread_lib",
        "//source/common/event:libevent_lib",
    ],
)

envoy_cc_library(
    name = "hot_restart_lib",
    srcs = envoy_select_hot_restart(["hot_restart_impl.cc"]),
    hdrs = envoy_select_hot_restart(["hot_restart_impl.h"]),
    deps = [
        "//include/envoy/api:os_sys_calls_interface",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:file_event_interface",
        "//include/envoy/server:hot_restart_interface",
        "//include/envoy/server:instance_interface",
        "//include/envoy/server:options_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:utility_lib",
        "//source/common/network:utility_lib",
        "//source/common/stats:stats_lib",
    ],
)

envoy_cc_library(
    name = "hot_restart_nop_lib",
    hdrs = ["hot_restart_nop_impl.h"],
    deps = [
        "//include/envoy/server:hot_restart_interface",
    ],
)

envoy_cc_library(
    name = "init_manager_lib",
    srcs = ["init_manager_impl.cc"],
    hdrs = ["init_manager_impl.h"],
    deps = [
        "//include/envoy/init:init_interface",
        "//source/common/common:assert_lib",
    ],
)

envoy_cc_library(
    name = "options_lib",
    srcs = ["options_impl.cc"],
    hdrs = ["options_impl.h"],
    external_deps = ["tclap"],
    deps = [
        "//include/envoy/network:address_interface",
        "//include/envoy/server:options_interface",
        "//source/common/common:macros",
        "//source/common/common:version_lib",
    ],
)

envoy_cc_library(
    name = "lds_api_lib",
    srcs = ["lds_api.cc"],
    hdrs = ["lds_api.h"],
    external_deps = ["envoy_lds"],
    deps = [
        ":lds_subscription_lib",
        "//include/envoy/config:subscription_interface",
        "//include/envoy/init:init_interface",
        "//include/envoy/server:listener_manager_interface",
        "//source/common/config:subscription_factory_lib",
        "//source/common/config:utility_lib",
    ],
)

envoy_cc_library(
    name = "lds_subscription_lib",
    srcs = ["lds_subscription.cc"],
    hdrs = ["lds_subscription.h"],
    external_deps = ["envoy_lds"],
    deps = [
        "//include/envoy/config:subscription_interface",
        "//source/common/common:assert_lib",
        "//source/common/config:lds_json_lib",
        "//source/common/config:utility_lib",
        "//source/common/http:rest_api_fetcher_lib",
        "//source/common/json:config_schemas_lib",
        "//source/common/json:json_validator_lib",
    ],
)

envoy_cc_library(
    name = "listener_manager_lib",
    srcs = ["listener_manager_impl.cc"],
    hdrs = ["listener_manager_impl.h"],
    external_deps = ["envoy_lds"],
    deps = [
        ":configuration_lib",
        ":drain_manager_lib",
        ":init_manager_lib",
        "//include/envoy/server:filter_config_interface",
        "//include/envoy/server:listener_manager_interface",
        "//include/envoy/server:worker_interface",
        "//source/common/config:utility_lib",
        "//source/common/network:listen_socket_lib",
        "//source/common/network:utility_lib",
        "//source/common/protobuf:utility_lib",
        "//source/common/ssl:context_config_lib",
    ],
)

envoy_cc_library(
    name = "server_lib",
    srcs = ["server.cc"],
    hdrs = ["server.h"],
    external_deps = ["envoy_bootstrap"],
    deps = [
        ":configuration_lib",
        ":connection_handler_lib",
        ":guarddog_lib",
        ":init_manager_lib",
        ":listener_manager_lib",
        ":test_hooks_lib",
        ":worker_lib",
        "//include/envoy/common:optional",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:signal_interface",
        "//include/envoy/event:timer_interface",
        "//include/envoy/network:dns_interface",
        "//include/envoy/server:drain_manager_interface",
        "//include/envoy/server:instance_interface",
        "//include/envoy/server:listener_manager_interface",
        "//include/envoy/server:options_interface",
        "//include/envoy/stats:stats_macros",
        "//include/envoy/tracing:http_tracer_interface",
        "//include/envoy/upstream:cluster_manager_interface",
        "//source/common/access_log:access_log_manager_lib",
        "//source/common/api:api_lib",
        "//source/common/common:utility_lib",
        "//source/common/common:version_lib",
        "//source/common/config:bootstrap_json_lib",
        "//source/common/local_info:local_info_lib",
        "//source/common/memory:stats_lib",
        "//source/common/protobuf:utility_lib",
        "//source/common/router:rds_lib",
        "//source/common/runtime:runtime_lib",
        "//source/common/singleton:manager_impl_lib",
        "//source/common/upstream:cluster_manager_lib",
        "//source/server/http:admin_lib",
    ],
)

envoy_cc_library(
    name = "test_hooks_lib",
    hdrs = ["test_hooks.h"],
)

envoy_cc_library(
    name = "watchdog_lib",
    srcs = ["watchdog_impl.cc"],
    hdrs = ["watchdog_impl.h"],
    deps = [
        "//include/envoy/common:time_interface",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/server:watchdog_interface",
        "//source/common/common:assert_lib",
    ],
)

envoy_cc_library(
    name = "worker_lib",
    srcs = ["worker_impl.cc"],
    hdrs = ["worker_impl.h"],
    deps = [
        ":connection_handler_lib",
        ":test_hooks_lib",
        "//include/envoy/api:api_interface",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:timer_interface",
        "//include/envoy/server:configuration_interface",
        "//include/envoy/server:guarddog_interface",
        "//include/envoy/server:listener_manager_interface",
        "//include/envoy/server:worker_interface",
        "//include/envoy/thread_local:thread_local_interface",
        "//source/common/common:thread_lib",
    ],
)
