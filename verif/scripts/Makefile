export TEST ?= test_pd

export SCRIPTS_DIR = $(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))
export CL_ROOT     = $(realpath $(SCRIPTS_DIR)/../..)
export TEST_NAME   = $(CL_ROOT)/verif/tests/$(TEST)

export SIM_ROOT = $(CL_ROOT)/verif/sim/$(SIMULATOR)
export SIM_DIR  = $(SIM_ROOT)/$(TEST)

all: make_sim_dir compile run

# surround path with quotes
MEM_PATH              ?= $(CL_ROOT)/verif/data/rv32ui-p-add.x
MEM_PATH_NOT_DIR			:= $(notdir $(MEM_PATH))
LINE_COUNT            ?= $(shell echo `wc -l < $(MEM_PATH)`)
MEM_PATH_STR          ?= \"$(abspath $(MEM_PATH))\"
MEM_DEPTH             ?= 1048576
TEST_VECTOR           ?= $(CL_ROOT)/verif/data/test_vector.x
TEST_VECTOR_STR       ?= \"$(TEST_VECTOR)\"
TRACE_FILE				    ?= $(MEM_PATH_NOT_DIR:x=trace)
VCD_FILE				      ?= $(MEM_PATH_NOT_DIR:x=vcd)
VCD_FILE_STR			    ?= \"$(VCD_FILE)\"
PATTERN_FILE          ?= $(MEM_PATH:x=pattern) # Replace MEM_PATH .x with .pattern by default
PATTERN_LINE_COUNT    ?= $(shell if [ ! -f $(PATTERN_FILE) ]; then echo -1; else echo `wc -l < $(PATTERN_FILE)`; fi)
PATTERN_FILE_STR      ?= \"$(abspath $(PATTERN_FILE))\"
PATTERN_DUMP_FILE			?= $(MEM_PATH_NOT_DIR:x=dump)# Replace MEM_PATH .x with .pattern by default
PATTERN_DUMP_FILE_STR ?= \"$(PATTERN_DUMP_FILE)\"
PATTERN_DUMP					?= 0
PATTERN_CHECK					?= 0
GEN_TRACE             ?= 1
TIMEOUT               ?= 5000
TRACE_FILE_STR        ?= \"$(TRACE_FILE)\"

WARN ?= 1

ifeq ($(WARN), 1)
WARN_OUTPUT = 2>&1 | tee output.log
WARN_CHECK  = cat $(SIM_DIR)/output.log | bash $(CL_ROOT)/verif/scripts/check_warnings.sh
else
WARN_OUTPUT = 
WARN_CHECK  = 
endif

EXTRA_PACKAGE_FILES := 

include ${PROJECT_ROOT}/common/verif/tb/scripts/Makefile.common.inc

