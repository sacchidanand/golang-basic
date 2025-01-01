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
