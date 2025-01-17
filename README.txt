AvrX for avr-gcc, version 2.6

10-Oct-2024 - Author Wei-Min Shen
	    - Fix a compile error in serialio.S for avr-gcc 12.0
	      for define SIG_UART_RECV and SIG_UART_DATA

19-Sep-2005 - Updated for WinAvr 3.4.3.
	    - Used new WinAvr makefile template.
	    - Added AvrXFifo facility
	    - Removed "serialio.S" from library as it is processor dependent.
	    - Renamed all assembly files from *.s to *.S to match GCC conventions.
	    - changed task function attribute to "noreturn" so frame variables would work.
	    - Modified select tasking primitives to work on both tasks and
	      interrupt handler.  The primitives also preserve the I flag across calls.
	    - Updated code for IAR per Steve krepelka. Removed avrio.h as a result.
	    - Put all changed & removed files into 2.6e subdirectory to facilitate
	      testing in case problems are found in the future.
	    - all samples & test cases built and run.

17-May-2004 - avrx_reschedule.s was broken (always has been): had to add "begin_critical"
    just prior to the "IntProlog" in AvrXYeild().
05-Jan-2004 - avrx_reschedule.s was broken (always has been): had to update & fix spelling
    of "AvrXYeild" -> AvrXYield.  Added the file to the library as well.
31-May-2002
Modifications, changes needed to sucessfully compile and run on the mega128
using test release 2 avrgcc128 compiler (alpha 3.1 release)

serialio.h  - new file, function prototypes
serialio.s  - Fixed interrupt handler names (used defines)
            - Fixed USART0 init (lots of renames for existing register
              and bits that got changed for no apparent reason)
monitor.s   - Fixed address handling in modify memory command. It used to wrap
              oddly (upper byte not being preserved)
avrx_generatesinglestepinterrupt.s
            - Those bit name changes again (CS00 -> CS0 for mega chip)
avrx_eeprom.s - Fixed use of EEARH instead of EEARL+1 so it will compile for
              smaller chips w/o error.

NB: With the new GCC compiler, the existing support for IAR compilers will
fail in the interrupt vector segment.  If you use IAR you will need to fix this on
your own.


8-June-2001

After executing a "make clean" the directory listing is as follows:

avrx-io.h               (IAR wrapper for io-avr.h)
avrx.h
avrx.inc
avrx.xlb                (IAR linker)
avrx_canceltimer.s
avrx_canceltimermessage.s
avrx_eeprom.s
avrx_halt.s
avrx_message.s
avrx_priority.s
avrx_recvmessage.s
avrx_resetsemaphore.s
avrx_semaphores.s
avrx_singlestep.s
avrx_starttimermessage.s
avrx_suspend.s
avrx_tasking.s
avrx_terminate.s
avrx_testsemaphore.s
avrx_timequeue.s
makefile
monitor.s
README.txt
serialio.s
avrx-signal.h           (IAR wrapper for sig-avr.h)
ioavr.h                 (IAR's version of io-avr.h)
avrx_generatesinglestepinterrupt.s
avrx-ctoasm.inc
avrx_iar_vect.s         (Avrx's interrupt table for IAR)


MAKEFILE instructions:

The makefile depends upon the environment variable AVRX being
set to the root directory of the AvrX distribution.  E.g. the parent
directory where this ReadMe.txt file is found.

make            - Will build both IAR and GCC libraries
make gcc
make iar
make clean      - will clean out the directory

ENVIRONMENT

The examples were developed and compiled under avr-gcc 3.0 (anything
higher than 2.97 should work) that can be found at:

http://combio.de/avr
http://www.avrfreaks.net

You need a copy of IAR Atmel AVR C/EC++ Compiler V2.25B/WIN or greater
to build the kernel and samples for IAR C.  The kernel is written to
conform to IAR A90 C compiler, but I don't have that compiler and
there will certainly be some code tweaking needed - mainly in alternate
directives, etc. the actual code should be compatible.


DISCLAIMER: I work with windows only.  Your milage may vary with Linux.
In particular, I try to keep file names consistant, but since windows
hides upper/lower case from me, I might have missed one or two.  Please
let me know of problems or suggestions or, better yet solutions to this
problem.

- Larryba@barello.net
