
# Configure catch3
include_directories(./catch3/)
add_library(catch3 SHARED ./catch3/catch_amalgamated.cpp)

# Add tests
add_executable(stockfish stockfish.cpp)
target_link_libraries(stockfish uciadapter catch3)
add_test(Stockfish stockfish)

add_executable(berserk berserk.cpp)
target_link_libraries(berserk uciadapter catch3)
add_test(Berserk berserk)