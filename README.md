
This is an example of using a bazel-generated directory as an input to a go_binary rule. 

```bash
go_directory_failure $ bazel run //:main
WARNING: Ignoring JAVA_HOME, because it must point to a JDK, not a JRE.
ERROR: /Users/davidmcnamee/dev/repro/go_directory_failure/BUILD.bazel:11:10: in srcs attribute of go_binary rule //:main: '//:generate' does not produce any go_binary srcs files (expected .go, .s, .S, .h, .c, .cc, .cpp, .cxx, .h, .hh, .hpp, .hxx, .inc, .m or .mm). Since this rule was created by the macro 'go_binary_macro', the error might have been caused by the macro implementation
ERROR: /Users/davidmcnamee/dev/repro/go_directory_failure/BUILD.bazel:11:10: Analysis of target '//:main' failed
ERROR: Analysis of target '//:main' failed; build aborted: 
INFO: Elapsed time: 0.178s
INFO: 0 processes.
FAILED: Build did NOT complete successfully (1 packages loaded, 3 targets configured)
ERROR: Build failed. Not running target
```

The same error occurs if you swap in `"mydir"` in place of `":generate"`, or if you use an intermediate go_library before passing to go_binary (i.e. `go_library(name = "intermediate", srcs = ["mydir"])`)
