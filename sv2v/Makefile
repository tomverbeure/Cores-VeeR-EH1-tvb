# verilator --cc -CFLAGS "-std=c++11" 
#	snapshots/default/common_defines.vh \ 
# 	/home/tom/projects/Cores-VeeR-EH1-tvb/design/include/veer_types.sv \ 
#	-I/home/tom/projects/Cores-VeeR-EH1-tvb/design/include \ 
#	-I/home/tom/projects/Cores-VeeR-EH1-tvb/design/lib  
# 	-Isnapshots/default \
#       -Wno-UNOPTFLAT \
#       -I/home/tom/projects/Cores-VeeR-EH1-tvb/testbench \
# 	-f /home/tom/projects/Cores-VeeR-EH1-tvb/testbench/flist \
#       /home/tom/projects/Cores-VeeR-EH1-tvb/testbench/tb_top.sv 
# 	/home/tom/projects/Cores-VeeR-EH1-tvb/testbench/ahb_sif.sv \
#       --top-module tb_top -exe test_tb_top.cpp --autoflush 

RV_ROOT = ../

PACKAGES = $(RV_ROOT)/snapshots/default/common_defines.vh
PACKAGES += $(RV_ROOT)/design/include/veer_types.sv

INCLUDES = -I$(RV_ROOT)/design/include
INCLUDES += -I$(RV_ROOT)/design/lib
INCLUDES += -I$(RV_ROOT)/snapshots/default

MODULES = $(RV_ROOT)/design/veer_wrapper.sv \
	$(RV_ROOT)/design/mem.sv \
	$(RV_ROOT)/design/pic_ctrl.sv \
	$(RV_ROOT)/design/veer.sv \
	$(RV_ROOT)/design/dma_ctrl.sv \
	$(RV_ROOT)/design/ifu/ifu_aln_ctl.sv \
	$(RV_ROOT)/design/ifu/ifu_compress_ctl.sv \
	$(RV_ROOT)/design/ifu/ifu_ifc_ctl.sv \
	$(RV_ROOT)/design/ifu/ifu_bp_ctl.sv \
	$(RV_ROOT)/design/ifu/ifu_ic_mem.sv \
	$(RV_ROOT)/design/ifu/ifu_mem_ctl.sv \
	$(RV_ROOT)/design/ifu/ifu_iccm_mem.sv \
	$(RV_ROOT)/design/ifu/ifu.sv \
	$(RV_ROOT)/design/dec/dec_decode_ctl.sv \
	$(RV_ROOT)/design/dec/dec_gpr_ctl.sv \
	$(RV_ROOT)/design/dec/dec_ib_ctl.sv \
	$(RV_ROOT)/design/dec/dec_tlu_ctl.sv \
	$(RV_ROOT)/design/dec/dec_trigger.sv \
	$(RV_ROOT)/design/dec/dec.sv \
	$(RV_ROOT)/design/exu/exu_alu_ctl.sv \
	$(RV_ROOT)/design/exu/exu_mul_ctl.sv \
	$(RV_ROOT)/design/exu/exu_div_ctl.sv \
	$(RV_ROOT)/design/exu/exu.sv \
	$(RV_ROOT)/design/lsu/lsu.sv \
	$(RV_ROOT)/design/lsu/lsu_clkdomain.sv \
	$(RV_ROOT)/design/lsu/lsu_addrcheck.sv \
	$(RV_ROOT)/design/lsu/lsu_lsc_ctl.sv \
	$(RV_ROOT)/design/lsu/lsu_stbuf.sv \
	$(RV_ROOT)/design/lsu/lsu_bus_buffer.sv \
	$(RV_ROOT)/design/lsu/lsu_bus_intf.sv \
	$(RV_ROOT)/design/lsu/lsu_ecc.sv \
	$(RV_ROOT)/design/lsu/lsu_dccm_mem.sv \
	$(RV_ROOT)/design/lsu/lsu_dccm_ctl.sv \
	$(RV_ROOT)/design/lsu/lsu_trigger.sv \
	$(RV_ROOT)/design/dbg/dbg.sv \
	$(RV_ROOT)/design/dmi/dmi_wrapper.v \
	$(RV_ROOT)/design/dmi/dmi_jtag_to_core_sync.v \
	$(RV_ROOT)/design/dmi/rvjtag_tap.sv \
	$(RV_ROOT)/design/lib/beh_lib.sv \
	$(RV_ROOT)/design/lib/mem_lib.sv

all: veer_sim.o

veer_conv.v: $(PACKAGES) $(MODULES) 
	time ~/tools/sv2v-Linux/sv2v --write=veer_conv.v $(INCLUDES) $(PACKAGES) $(MODULES)

veer_sim.cpp: veer_conv.v
	time yosys -s veer_synth.ys

veer_sim.o: veer_sim.cpp
	#time g++ --save-temps -Q -ftime-report-details -c -I `yosys-config --datdir`/include veer_sim.cpp -o veer_sim.o
	time clang++ -c -I `yosys-config --datdir`/include veer_sim.cpp 

clean:
	\rm -fr veer_conv.v veer_sim.cpp veer_sim.o
