add_library(japi OBJECT
	japi.c
)
target_include_directories(japi PRIVATE
	..
	../../common
	../../daemons/qmaster
	../../libs/evm
	../../libs/uti
	../cull
	../sgeobj
)

add_library(drmaa SHARED
	drmaa.c
	drmaa2_list_dict.c
)
target_include_directories(drmaa PRIVATE
	..
	../../clients/common
	../../common
	../../daemons/qmaster
	../../libs/evm
	../../libs/uti
	../gdi
	../cull
	../sgeobj
)
target_link_libraries(drmaa PRIVATE
	$<TARGET_OBJECTS:japi>
	comm
	commlists
	cull
	evc
	gdi
	parse_job_cull
	parse_qsub
	read_defaults
	sge_mt_init
	sge_options
	sgeobj
	sgeobjd
	uti
)
target_link_options(drmaa PRIVATE
	-Wl,--version-script=${CMAKE_CURRENT_SOURCE_DIR}/drmaa.lds
)
