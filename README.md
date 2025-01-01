# golang-basic
golang-learning


# shell command to count words
bash-3.2$ time wc -w moby.txt
  215822 moby.txt

real    0m0.014s
user    0m0.006s
sys     0m0.004s
----------------------------------------------------------------

# Our program to read file and count words
# compile
go build

# run it
bash-3.2$ time ./words moby.txt 
2025/01/01 15:07:45 profile: cpu profiling enabled, cpu.pprof
"moby.txt": 181392 words
2025/01/01 15:07:45 profile: cpu profiling disabled, cpu.pprof

real    0m0.964s
user    0m0.192s
sys     0m0.490s
----------------------------------------------------------------

# CPU profiling
bash-3.2$ go tool pprof -http=:8080 cpu.pprof
Serving web UI on http://localhost:8080
----------------------------------------------------------------

#Change-1
With New changes of introducing buffered io

bash-3.2$ time ./words moby.txt 
2025/01/01 15:11:29 profile: cpu profiling enabled, cpu.pprof
"moby.txt": 181392 words
2025/01/01 15:11:29 profile: cpu profiling disabled, cpu.pprof

real    0m0.708s
user    0m0.036s
sys     0m0.012s
----------------------------------------------------------------

#Change-2
Use memory profiling with default rate 4096


bash-3.2$ time ./words moby.txt 
2025/01/01 15:23:46 profile: memory profiling enabled (rate 4096), mem.pprof
"moby.txt": 181392 words
2025/01/01 15:23:47 profile: memory profiling disabled, mem.pprof

real    0m1.095s
user    0m0.198s
sys     0m0.444s
bash-3.2$ go tool pprof -http=:8080 mem.pprof
Serving web UI on http://localhost:8080

With fix and updated mem profile rate = 1


bash-3.2$ time ./words moby.txt 
2025/01/01 15:42:15 profile: memory profiling enabled (rate 1), mem.pprof
"moby.txt": 181392 words
2025/01/01 15:42:15 profile: memory profiling disabled, mem.pprof

real    0m0.091s
user    0m0.020s
sys     0m0.017s

bash-3.2$ time wc moby.txt 
   22655  215822 1254132 moby.txt

real    0m0.055s
user    0m0.005s
sys     0m0.006s

----------------------------------------------------------------