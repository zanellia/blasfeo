###################################################################################################
#                                                                                                 #
# This file is part of BLASFEO.                                                                   #
#                                                                                                 #
# BLASFEO -- BLAS for embedded optimization.                                                      #
# Copyright (C) 2019 by Gianluca Frison.                                                          #
# Developed at IMTEK (University of Freiburg) under the supervision of Moritz Diehl.              #
# All rights reserved.                                                                            #
#                                                                                                 #
# The 2-Clause BSD License                                                                        #
#                                                                                                 #
# Redistribution and use in source and binary forms, with or without                              #
# modification, are permitted provided that the following conditions are met:                     #
#                                                                                                 #
# 1. Redistributions of source code must retain the above copyright notice, this                  #
#    list of conditions and the following disclaimer.                                             #
# 2. Redistributions in binary form must reproduce the above copyright notice,                    #
#    this list of conditions and the following disclaimer in the documentation                    #
#    and/or other materials provided with the distribution.                                       #
#                                                                                                 #
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND                 #
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED                   #
# WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE                          #
# DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR                 #
# ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES                  #
# (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;                    #
# LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND                     #
# ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT                      #
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS                   #
# SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.                                    #
#                                                                                                 #
# Author: Gianluca Frison, gianluca.frison (at) imtek.uni-freiburg.de                             #
#                                                                                                 #
###################################################################################################

include ../Makefile.rule

OBJS =

OBJS += blasfeo_stdlib.o

ifeq ($(LA), HIGH_PERFORMANCE)

ifeq ($(TARGET), X64_INTEL_HASWELL)
OBJS += d_aux_lib4.o
OBJS += s_aux_lib8.o
OBJS += m_aux_lib48.o
endif

ifeq ($(TARGET), X64_INTEL_SANDY_BRIDGE)
OBJS += d_aux_lib4.o
OBJS += s_aux_lib8.o
OBJS += m_aux_lib48.o
endif

ifeq ($(TARGET), X64_INTEL_CORE)
OBJS += d_aux_lib4.o
OBJS += s_aux_lib4.o
OBJS += m_aux_lib44.o
endif

ifeq ($(TARGET), X64_AMD_BULLDOZER)
OBJS += d_aux_lib4.o
OBJS += s_aux_lib4.o
OBJS += m_aux_lib44.o
endif

ifeq ($(TARGET), X86_AMD_JAGUAR)
OBJS += d_aux_lib4.o
OBJS += s_aux_lib4.o
OBJS += m_aux_lib44.o
endif

ifeq ($(TARGET), X86_AMD_BARCELONA)
OBJS += d_aux_lib4.o
OBJS += s_aux_lib4.o
OBJS += m_aux_lib44.o
endif

ifeq ($(TARGET), $(filter $(TARGET), ARMV8A_ARM_CORTEX_A57 ARMV8A_ARM_CORTEX_A53))
OBJS += d_aux_lib4.o
OBJS += s_aux_lib4.o
OBJS += m_aux_lib44.o
endif

ifeq ($(TARGET), $(filter $(TARGET), ARMV7A_ARM_CORTEX_A15 ARMV7A_ARM_CORTEX_A9 ARMV7A_ARM_CORTEX_A7))
OBJS += d_aux_lib4.o
OBJS += s_aux_lib4.o
OBJS += m_aux_lib44.o
endif

ifeq ($(TARGET), GENERIC)
OBJS += d_aux_lib4.o
OBJS += s_aux_lib4.o
OBJS += m_aux_lib44.o
endif

else # LA_REFERENCE | LA_EXTERNAL_BLAS_WRAPPER

OBJS += d_aux_lib.o
OBJS += s_aux_lib.o
OBJS += m_aux_lib.o

endif # LA choice

ifeq ($(TESTING_MODE), 1)
#testing against reference
OBJS += d_aux_libref.o
OBJS += s_aux_libref.o
endif


#ext dep
ifeq ($(EXT_DEP), 1)

ifeq ($(LA), HIGH_PERFORMANCE)
OBJS += d_aux_ext_dep_lib4.o
OBJS += s_aux_ext_dep_lib4.o
endif
OBJS += d_aux_ext_dep_lib.o
OBJS += s_aux_ext_dep_lib.o
OBJS += v_aux_ext_dep_lib.o
OBJS += i_aux_ext_dep_lib.o
OBJS += timing.o

ifeq ($(TESTING_MODE), 1)
OBJS += d_aux_libref.o
OBJS += s_aux_libref.o
OBJS += d_aux_ext_dep_libref.o
OBJS += s_aux_ext_dep_libref.o
endif

endif


obj: $(OBJS)

clean:
	rm -f *.o
	rm -f *.s
	rm -f *.gcda
	rm -f *.gcno
	rm -f *.gcov

d_aux_lib.o: d_aux_lib.c x_aux_lib.c
s_aux_lib.o: s_aux_lib.c x_aux_lib.c
d_aux_ext_dep_lib.o: d_aux_ext_dep_lib.c x_aux_ext_dep_lib0.c x_aux_ext_dep_lib.c
s_aux_ext_dep_lib.o: s_aux_ext_dep_lib.c x_aux_ext_dep_lib0.c x_aux_ext_dep_lib.c
d_aux_ext_dep_lib4.o: d_aux_ext_dep_lib4.c x_aux_ext_dep_lib4.c
s_aux_ext_dep_lib4.o: s_aux_ext_dep_lib4.c x_aux_ext_dep_lib4.c
