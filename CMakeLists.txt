# Copyright (©) 2024-2025  Frosty515

# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <https://www.gnu.org/licenses/>.

cmake_minimum_required(VERSION 3.20)

project(Frost64 C CXX ASM_NASM)

if (NOT DEFINED BUILD_CONFIG)
    set(BUILD_CONFIG "Release")
endif()

if (NOT DEFINED BUILD_ARCHITECTURE)
    set(BUILD_ARCHITECTURE "x86_64")
endif()

add_custom_target(distinstall
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:Emulator> /usr/bin/frost64-emu
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:Assembler> /usr/bin/frost64-asm
    COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:Disassembler> /usr/bin/frost64-dasm
    DEPENDS Emulator Assembler Disassembler
)

add_subdirectory(LibArch)
add_subdirectory(LibCommon)
add_subdirectory(Assembler)
add_subdirectory(Disassembler)
add_subdirectory(Emulator)