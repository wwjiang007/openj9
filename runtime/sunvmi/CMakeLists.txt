################################################################################
# Copyright IBM Corp. and others 2017
#
# This program and the accompanying materials are made available under
# the terms of the Eclipse Public License 2.0 which accompanies this
# distribution and is available at https://www.eclipse.org/legal/epl-2.0/
# or the Apache License, Version 2.0 which accompanies this distribution and
# is available at https://www.apache.org/licenses/LICENSE-2.0.
#
# This Source Code may also be made available under the following
# Secondary Licenses when the conditions for such availability set
# forth in the Eclipse Public License, v. 2.0 are satisfied: GNU
# General Public License, version 2 with the GNU Classpath
# Exception [1] and GNU General Public License, version 2 with the
# OpenJDK Assembly Exception [2].
#
# [1] https://www.gnu.org/software/classpath/license.html
# [2] https://openjdk.org/legal/assembly-exception.html
#
# SPDX-License-Identifier: EPL-2.0 OR Apache-2.0 OR GPL-2.0-only WITH Classpath-exception-2.0 OR GPL-2.0-only WITH OpenJDK-assembly-exception-1.0
################################################################################

set(OMR_ENHANCED_WARNINGS OFF)

add_tracegen(sunvmi.tdf)

j9vm_add_library(sunvmi STATIC
	sunvmi.c
	${CMAKE_CURRENT_BINARY_DIR}/ut_sunvmi.c
)

target_include_directories(sunvmi
	PRIVATE
		../jcl
		${CMAKE_CURRENT_BINARY_DIR}
)

target_link_libraries(sunvmi
	PRIVATE
		j9vm_interface
		j9vm_gc_includes

		j9util
)

# Note we need to make sure the gc hookgen/tracegen headers exist before we start compiling
add_dependencies(sunvmi omrgc_hookgen omrgc_tracegen)
