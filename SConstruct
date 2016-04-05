# Top SConstruct file

tool_path = '/opt/freddie-arm-5_3/'
cross_prefix = tool_path+'bin/arm-none-eabi-'

cc_flags = Split('''
		-Wall -Wextra 
		-ffunction-sections -fdata-sections 
		-fno-common -MD 
		''')
cxx_flags = Split('''
		-x c++ -pipe
		-Wall -Wextra -Winline
		-Wcast-align -Wcast-qual -Wshadow
		-fno-exceptions -fno-rtti
		-ffunction-sections -fdata-sections
		-funsigned-bitfields -fshort-enums
		-pedantic -MD
		''')
	
as_flags = Split('-x assembler-with-cpp -Wa,-ahlms=$(<:.s=.lst),--gstabs -MD -D_ASSEMBLER_ -mthumb')

ld_flags = Split('''
		-Wall
		--static
		-nostartfiles
		-Wl,--gc-sections
		''')

ar_flags=Split('rcs')

opti_flags = Split('-Os -fomit-frame-pointer -fexpensive-optimizations -g')

cm0_dir = 'Lib/cortex_m0plus/'
#cm3_dir = 'Lib/cortex_m3/'
cm4_dir = 'Lib/cortex_m4/'
cm4f_dir = 'Lib/cortex_m4f/'
cm7_dir = 'Lib/cortex_m7/'
cm7f_sp_dir = 'Lib/cortex_m7f_sp/'
cm7f_dp_dir ='Lib/cortex_m7f_dp/'
inc_dir = 'Include/'
src_dir = 'DSP_Lib/Source/'

scr_file = 'SConscript'

env = Environment(
			CCFLAGS=cc_flags+opti_flags,
			CC=cross_prefix+'gcc',
			CXXFLAGS=cxx_flags+opti_flags,
			CXX=cross_prefix+'gcc',
			LINKFLAGS=ld_flags,
			LINK=cross_prefix+'gcc',
			ASFLAGS=as_flags+opti_flags,
			AS=cross_prefix+'gcc',
			CPPPATH=Split(inc_dir+' '+tool_path+'/arm-none-eabi/include'),
			AR=cross_prefix+'ar',
			ARFLAGS=ar_flags,
			RANLIB=cross_prefix+'ranlib'
		)

cm0_sw = Split('-mcpu=cortex-m0plus -mfloat-abi=soft -mthumb')
cm0_env = env.Clone()
cm0_env.Append(CCFLAGS=cm0_sw,CXXFLAGS=cm0_sw,LINKFLAGS=cm0_sw,ASFLAGS=cm0_sw,CPPDEFINES=['ARM_MATH_CM0PLUS'])


cm4_sw = Split('-mcpu=cortex-m4 -mfloat-abi=soft -mfpu=fpv4-sp-d16 -mthumb')
cm4_env = env.Clone()
cm4_env.Append(CCFLAGS=cm4_sw,CXXFLAGS=cm4_sw,LINKFLAGS=cm4_sw,ASFLAGS=cm4_sw,CPPDEFINES=['ARM_MATH_CM4'])


cm4f_sw = Split('-mcpu=cortex-m4 -mfloat-abi=hard -mfpu=fpv4-sp-d16 -mthumb')
cm4f_env = env.Clone()
cm4f_env.Append(CCFLAGS=cm4f_sw,CXXFLAGS=cm4f_sw,LINKFLAGS=cm4f_sw,ASFLAGS=cm4f_sw,CPPDEFINES=['ARM_MATH_CM4','__FPU_PRESENT'])


cm7_sw = Split('-mcpu=cortex-m7 -mfloat-abi=soft -mthumb')
cm7_env = env.Clone()
cm7_env.Append(CCFLAGS=cm7_sw,CXXFLAGS=cm7_sw,LINKFLAGS=cm7_sw,ASFLAGS=cm7_sw,CPPDEFINES=['ARM_MATH_CM7'])


cm7f_sp_sw = Split('-mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv4-sp-d16 -mthumb')
cm7f_sp_env = env.Clone()
cm7f_sp_env.Append(CCFLAGS=cm7f_sp_sw,CXXFLAGS=cm7f_sp_sw,LINKFLAGS=cm7f_sp_sw,ASFLAGS=cm7f_sp_sw,CPPDEFINES=['ARM_MATH_CM7','__FPU_PRESENT'])


cm7f_dp_sw = Split('-mcpu=cortex-m7 -mfloat-abi=hard -mfpu=fpv5-sp-d16 -mthumb')
cm7f_dp_env = env.Clone()
cm7f_dp_env.Append(CCFLAGS=cm7f_dp_sw,CXXFLAGS=cm7f_dp_sw,LINKFLAGS=cm7f_dp_sw,ASFLAGS=cm7f_dp_sw,CPPDEFINES=['ARM_MATH_CM7','__FPU_PRESENT'])

env.SConscript(src_dir+scr_file, exports={'env':cm0_env,'cm_postfix':'M0plus'}, variant_dir=cm0_dir, duplicate=0)
env.SConscript(src_dir+scr_file, exports={'env':cm4_env,'cm_postfix':'M4'}, variant_dir=cm4_dir, duplicate=0)
env.SConscript(src_dir+scr_file, exports={'env':cm4f_env,'cm_postfix':'M4F'}, variant_dir=cm4f_dir, duplicate=0)
env.SConscript(src_dir+scr_file, exports={'env':cm7_env,'cm_postfix':'M7'}, variant_dir=cm7_dir, duplicate=0)
env.SConscript(src_dir+scr_file, exports={'env':cm7f_sp_env,'cm_postfix':'M7Fsp'}, variant_dir=cm7f_sp_dir, duplicate=0)
env.SConscript(src_dir+scr_file, exports={'env':cm7f_dp_env,'cm_postfix':'M7Fdp'}, variant_dir=cm7f_dp_dir, duplicate=0)


Clean('depend.d',Glob(cm0_dir+'*/*.d')
		+Glob(cm4_dir+'*/*.d')
		+Glob(cm4f_dir+'*/*.d')
		+Glob(cm7_dir+'*/*.d')
		+Glob(cm7f_sp_dir+'*/*.d')
		+Glob(cm7f_dp_dir+'*/*.d')
		)
