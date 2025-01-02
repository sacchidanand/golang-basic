# Shell command to count words

bash-3.2$ time wc -w moby.txt
  215822 moby.txt

- real    0m0.014s
- user    0m0.006s
- sys     0m0.004s

----------------------------------------------------------------

# Our program to read file and count words
# compile
go build

# run it
bash-3.2$ time ./words moby.txt 

2025/01/01 15:07:45 profile: cpu profiling enabled, cpu.pprof

"moby.txt": 181392 words

2025/01/01 15:07:45 profile: cpu profiling disabled, cpu.pprof

- real    0m0.964s
- user    0m0.192s
- sys     0m0.490s
----------------------------------------------------------------

# CPU profiling
bash-3.2$ go tool pprof -http=:8080 cpu.pprof

Serving web UI on http://localhost:8080
----------------------------------------------------------------

# Change-1
With New changes of introducing buffered io

bash-3.2$ time ./words moby.txt 

2025/01/01 15:11:29 profile: cpu profiling enabled, cpu.pprof

"moby.txt": 181392 words

2025/01/01 15:11:29 profile: cpu profiling disabled, cpu.pprof

- real    0m0.708s
- user    0m0.036s
- sys     0m0.012s
----------------------------------------------------------------

# Memory Profiling

# Change-2
Use memory profiling with default rate 4096


bash-3.2$ time ./words moby.txt 

2025/01/01 15:23:46 profile: memory profiling enabled (rate 4096), mem.pprof

"moby.txt": 181392 words

2025/01/01 15:23:47 profile: memory profiling disabled, mem.pprof

- real    0m1.095s
- user    0m0.198s
- sys     0m0.444s

bash-3.2$ go tool pprof -http=:8080 mem.pprof

Serving web UI on http://localhost:8080

With fix and updated mem profile rate = 1


bash-3.2$ time ./words moby.txt 

2025/01/01 15:42:15 profile: memory profiling enabled (rate 1), mem.pprof

"moby.txt": 181392 words

2025/01/01 15:42:15 profile: memory profiling disabled, mem.pprof

- real    0m0.091s
- user    0m0.020s
- sys     0m0.017s

bash-3.2$ time wc moby.txt 

   22655  215822 1254132 moby.txt

- real    0m0.055s
- user    0m0.005s
- sys     0m0.006s

----------------------------------------------------------------

# Trace Profiling
mandelbrot.png code analysis

# Option-1 Single threaded Seq execution

bash-3.2$ go build; time ./tracer

2025/01/02 13:41:42 profile: trace enabled, trace.out

2025/01/02 13:41:46 profile: trace disabled, trace.out

- real    0m3.826s
- user    0m3.233s
- sys     0m0.105s

bash-3.2$ go tool trace trace.out 

----------------------------------------------------------------

# Option-2 px execution

bash-3.2$ time ./tracer -mode px

2025/01/02 13:48:05 profile: trace enabled, trace.out

2025/01/02 13:48:07 profile: trace disabled, trace.out

- real    0m2.098s
- user    0m6.549s
- sys     0m0.643s

----------------------------------------------------------------

# Option-3 row execution

bash-3.2$ time ./tracer -mode row

2025/01/02 13:48:45 profile: trace enabled, trace.out

2025/01/02 13:48:46 profile: trace disabled, trace.out

- real    0m1.194s
- user    0m4.002s
- sys     0m0.027s

----------------------------------------------------------------

# Option-4 workers execution

bash-3.2$ time ./tracer -mode workers -workers=8

2025/01/02 13:49:35 profile: trace enabled, trace.out

2025/01/02 13:49:38 profile: trace disabled, trace.out

- real    0m3.535s
- user    0m5.985s
- sys     0m2.033s