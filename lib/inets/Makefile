#
# %CopyrightBegin%
#
# Copyright Ericsson AB 1996-2011. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# %CopyrightEnd%
#
#
include $(ERL_TOP)/make/target.mk
include $(ERL_TOP)/make/$(TARGET)/otp.mk

# ----------------------------------------------------
# Macros
# ----------------------------------------------------

SUB_DIRECTORIES = src examples priv doc/src 

include vsn.mk
VSN = $(INETS_VSN)

SPECIAL_TARGETS = 

DIA_PLT      = ./priv/plt/$(APPLICATION).plt
DIA_ANALYSIS = $(basename $(DIA_PLT)).dialyzer_analysis


# ----------------------------------------------------
# Default Subdir Targets
# ----------------------------------------------------
include $(ERL_TOP)/make/otp_subdir.mk

.PHONY: info gclean dialyzer dialyzer_plt dclean

info:
	@echo "OS:        $(OS)"
	@echo "DOCB:      $(DOCB)"
	@echo ""
	@echo "INETS_VSN: $(INETS_VSN)"
	@echo "APP_VSN:   $(APP_VSN)"
	@echo ""
	@echo "DIA_PLT:      $(DIA_PLT)"
	@echo "DIA_ANALYSIS: $(DIA_ANALYSIS)"
	@echo ""

gclean: 
	git clean -fXd

dclean:
	rm -f $(DIA_PLT)
	rm -f $(DIA_ANALYSIS)

dialyzer_plt: $(DIA_PLT)

$(DIA_PLT): 
	@echo "Building $(APPLICATION) plt file"
	@dialyzer --build_plt \
                  --output_plt $@ \
                  -r ../$(APPLICATION)/ebin \
                  --output $(DIA_ANALYSIS) \
                  --verbose

dialyzer: $(DIA_PLT)
	@echo "Running dialyzer on $(APPLICATION)"
	@dialyzer --plt $< \
                  ../$(APPLICATION)/ebin \
                  --verbose
