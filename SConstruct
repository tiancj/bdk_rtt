import os
import sys
import rtconfig
from rtconfig import RTT_ROOT

sys.path = sys.path + [os.path.join(RTT_ROOT, 'tools')]
from building import *

sys.path = sys.path + [os.path.join(RTT_ROOT, 'tools')]
from building import *

TARGET = 'rtthread.' + rtconfig.TARGET_EXT

env = Environment(tools = ['mingw'],
    AS = rtconfig.AS, ASFLAGS = rtconfig.AFLAGS,
    CC = rtconfig.CC, CCFLAGS = rtconfig.CFLAGS,
    CXX = rtconfig.CC, CXXFLAGS = rtconfig.CXXFLAGS,
    AR = rtconfig.AR, ARFLAGS = '-rc',
    LINK = rtconfig.LINK, LINKFLAGS = rtconfig.LFLAGS)
env.PrependENVPath('PATH', rtconfig.EXEC_PATH)

# add --start-group and --end-group for GNU GCC
if rtconfig.PLATFORM == 'gcc':
    env['LINKCOM'] = '$LINK -o $TARGET $LINKFLAGS $__RPATH $SOURCES $_LIBDIRFLAGS -Wl,--start-group $_LIBFLAGS -Wl,--end-group'

Export('RTT_ROOT')
Export('rtconfig')

# prepare building environment
objs = PrepareBuilding(env, RTT_ROOT, has_libcpu=True)

# make a building
DoBuilding(env, TARGET, objs)
