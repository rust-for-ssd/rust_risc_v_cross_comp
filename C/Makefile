default: dota

main.o: main.c
	riscv64-none-elf-gcc -c -g -O0 -mcmodel=medany -march=rv64id -mabi=lp64d -ffreestanding -o main.o main.c

start.o: start.s
	riscv64-none-elf-gcc -c -g -O0 -mcmodel=medany -march=rv64id -mabi=lp64d -ffreestanding -o start.o start.s

doto:
	cp ../target-obj/riscv64gc-unknown-none-elf/debug/deps/*.o ./rust_o/
	riscv64-none-elf-ld -T link.ld -m elf64lriscv -o doto.elf main.o start.o ./rust_o/*.o

dota:
	riscv64-none-elf-ld -T link.ld -m elf64lriscv -o dota.elf main.o start.o ../target/riscv64gc-unknown-none-elf/debug/librust_risc_v_cross_comp.a

run_dota:
	qemu-system-riscv64 -machine virt -serial 'mon:stdio' -nographic -bios ./dota.elf

run_doto:
	qemu-system-riscv64 -machine virt -serial 'mon:stdio' -nographic -bios ./doto.elf

extract_dota:
	riscv64-none-elf-ar x ../target/riscv64gc-unknown-none-elf/debug/librust_risc_v_cross_comp.a

clean:
	rm *.o
	rm ./rust_o/*.o
	rm *.elf
