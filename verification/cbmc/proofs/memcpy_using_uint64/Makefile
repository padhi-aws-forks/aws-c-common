# Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved.
# SPDX-License-Identifier: Apache-2.0.

###########
# Max needs to be big enough to have multiple loop unrollings to have full coverage
# 160 is well larger than that, and still completes quite fast: ~ 40s
MAX = 160
DEFINES += -DMAX=$(MAX)

UNWINDSET += memcpy_impl.0:$(shell echo $$(($(MAX) + 1)))
UNWINDSET += memcpy_using_uint64_impl.0:$(shell echo $$(( $$(( $(MAX) / 8 )) + 1)))

CBMCFLAGS +=

HARNESS_ENTRY = memcpy_using_uint64_harness
HARNESS_FILE = $(HARNESS_ENTRY).c

PROOF_SOURCES += $(HARNESS_FILE)
PROOF_SOURCES += $(PROOF_SOURCE)/utils.c

PROOF_SOURCES += $(PROOF_STUB)/memcpy_override.c
PROOF_SOURCES += $(PROOF_STUB)/memcpy_using_uint64.c

# The actual implementation that we're proving comes from .inl files
# that the stubs pull in. Link against an empty file, since we're not
# using any other files from c-common.
PROJECT_SOURCES += $(PROOF_STUB)/empty-source-file.c

###########

include ../Makefile.common
