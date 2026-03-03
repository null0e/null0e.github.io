```
#define _GNU_SOURCE 1

#include <stdlib.h>
#include <stdint.h>
#include <stdbool.h>
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <string.h>
#include <time.h>
#include <errno.h>
#include <assert.h>
#include <libgen.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <sys/socket.h>
#include <sys/wait.h>
#include <sys/signal.h>
#include <sys/mman.h>
#include <sys/ioctl.h>
#include <sys/sendfile.h>
#include <sys/prctl.h>
#include <sys/personality.h>
#include <arpa/inet.h>

void win()
{
    char flag[256];
    int flag_fd;
    int flag_length;

    flag_fd = open("/flag", 0);
    if (flag_fd < 0)
    {
        printf("\n  ERROR: Failed to open the flag -- %s!\n", strerror(errno));
        if (geteuid() != 0)
        {
            printf("  Your effective user id is not 0!\n");
            printf("  You must directly run the suid binary in order to have the correct permissions!\n");
        }
        exit(-1);
    }
    flag_length = read(flag_fd, flag, sizeof(flag));
    if (flag_length <= 0)
    {
        printf("\n  ERROR: Failed to read the flag -- %s!\n", strerror(errno));
        exit(-1);
    }
    write(1, flag, flag_length);
    printf("\n\n");
}

void read_exact(int fd, void *dst, int size, char *msg, int exitcode)
{
    int n = read(fd, dst, size);
    if (n != size)
    {
        fprintf(stderr, msg);
        fprintf(stderr, "\n");
        exit(exitcode);
    }
}

char desired_output[] = "\x1b[38;2;255;255;255m.\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m.\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m/\x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;233;108;053m|\x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m|\x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;071;012;011m \x1b[0m\x1b[38;2;071;012;011m \x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;192;206;171m_\x1b[0m\x1b[38;2;192;206;171m_\x1b[0m\x1b[38;2;192;206;171m_\x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m_\x1b[0m\x1b[38;2;091;055;051m_\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m_\x1b[0m\x1b[38;2;091;055;051m_\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;233;108;053m|\x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m|\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m|\x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;071;012;011m \x1b[0m\x1b[38;2;071;012;011m/\x1b[0m\x1b[38;2;071;012;011m \x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;192;206;171m|\x1b[0m\x1b[38;2;192;206;171m_\x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;192;206;171m_\x1b[0m\x1b[38;2;192;206;171m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m\\\x1b[0m\x1b[38;2;091;055;051m/\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;233;108;053m \x1b[0m\x1b[38;2;233;108;053m\\\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m_\x1b[0m\x1b[38;2;233;108;053m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;071;012;011m|\x1b[0m\x1b[38;2;071;012;011m \x1b[0m\x1b[38;2;071;012;011m(\x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;192;206;171m|\x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;192;206;171m|\x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m\\\x1b[0m\x1b[38;2;091;055;051m/\x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;071;012;011m \x1b[0m\x1b[38;2;071;012;011m\\\x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m_\x1b[0m\x1b[38;2;071;012;011m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;192;206;171m|\x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;192;206;171m|\x1b[0m\x1b[38;2;192;206;171m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;192;206;171m|\x1b[0m\x1b[38;2;192;206;171m_\x1b[0m\x1b[38;2;192;206;171m_\x1b[0m\x1b[38;2;192;206;171m_\x1b[0m\x1b[38;2;192;206;171m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m_\x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m \x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;091;055;051m_\x1b[0m\x1b[38;2;091;055;051m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;000;000;000m \x1b[0m\x1b[38;2;255;255;255m|\x1b[0m\x1b[38;2;255;255;255m'\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m-\x1b[0m\x1b[38;2;255;255;255m'\x1b[0m\x00";

struct cimg_header
{
    char magic_number[4];
    uint16_t version;
    uint8_t width;
    uint8_t height;
} __attribute__((packed));

typedef struct
{
    uint8_t ascii;
} pixel_bw_t;
#define COLOR_PIXEL_FMT "\x1b[38;2;%03d;%03d;%03dm%c\x1b[0m"
typedef struct
{
    uint8_t r;
    uint8_t g;
    uint8_t b;
    uint8_t ascii;
} pixel_color_t;
typedef pixel_color_t pixel_t;

typedef struct
{
    union
    {
        char data[24];
        struct term_str_st
        {
            char color_set[7];   // \x1b[38;2;
            char r[3];          // 255
            char s1;            // ;
            char g[3];          // 255
            char s2;            // ;
            char b[3];          // 255
            char m;            // m
            char c;             // X
            char color_reset[4];     // \x1b[0m
        } str;
    };
} term_pixel_t;

struct cimg
{
    struct cimg_header header;
    unsigned num_pixels;
    term_pixel_t *framebuffer;
};

#define CIMG_NUM_PIXELS(cimg) ((cimg)->header.width * (cimg)->header.height)
#define CIMG_DATA_SIZE(cimg) (CIMG_NUM_PIXELS(cimg) * sizeof(pixel_t))
#define CIMG_FRAMEBUFFER_PIXELS(cimg) ((cimg)->header.width * (cimg)->header.height)
#define CIMG_FRAMEBUFFER_SIZE(cimg) (CIMG_FRAMEBUFFER_PIXELS(cimg) * sizeof(term_pixel_t))

void display(struct cimg *cimg, pixel_t *data)
{
    int idx = 0;
    for (int y = 0; y < cimg->header.height; y++)
    {
        for (int x = 0; x < cimg->header.width; x++)
        {
            idx = (0+y)*((cimg)->header.width) + ((0+x)%((cimg)->header.width));
            char emit_tmp[24+1];
            snprintf(emit_tmp, sizeof(emit_tmp), "\x1b[38;2;%03d;%03d;%03dm%c\x1b[0m", data[y * cimg->header.width + x].r, data[y * cimg->header.width + x].g, data[y * cimg->header.width + x].b, data[y * cimg->header.width + x].ascii);
            memcpy((cimg)->framebuffer[idx%(cimg)->num_pixels].data, emit_tmp, 24);

        }
    }

    for (int i = 0; i < cimg->header.height; i++)
    {
        write(1, cimg->framebuffer+i*cimg->header.width, sizeof(term_pixel_t)*cimg->header.width);
        write(1, "\x1b[38;2;000;000;000m\n\x1b[0m", 24);
    }
}

struct cimg *initialize_framebuffer(struct cimg *cimg)
{
    cimg->num_pixels = CIMG_FRAMEBUFFER_PIXELS(cimg);
    cimg->framebuffer = malloc(CIMG_FRAMEBUFFER_SIZE(cimg)+1);
    if (cimg->framebuffer == NULL)
    {
        puts("ERROR: Failed to allocate memory for the framebuffer!");
        exit(-1);
    }
    for (int idx = 0; idx < cimg->num_pixels; idx += 1)
    {
        char emit_tmp[24+1];
        snprintf(emit_tmp, sizeof(emit_tmp), "\x1b[38;2;%03d;%03d;%03dm%c\x1b[0m", 255, 255, 255, ' ');
        memcpy(cimg->framebuffer[idx].data, emit_tmp, 24);

    }

    return cimg;
}

void __attribute__ ((constructor)) disable_buffering()
{
    setvbuf(stdin, NULL, _IONBF, 0);
    setvbuf(stdout, NULL, _IONBF, 1);
}

int main(int argc, char **argv, char **envp)
{

    struct cimg cimg = { 0 };
    cimg.framebuffer = NULL;
    int won = 1;

    if (argc > 1)
    {
        if (strcmp(argv[1]+strlen(argv[1])-5, ".cimg"))
        {
            printf("ERROR: Invalid file extension!");
            exit(-1);
        }
        dup2(open(argv[1], O_RDONLY), 0);
    }

    read_exact(0, &cimg.header, sizeof(cimg.header), "ERROR: Failed to read header!", -1);

    if (cimg.header.magic_number[0] != 'c' || cimg.header.magic_number[1] != 'I' || cimg.header.magic_number[2] != 'M' || cimg.header.magic_number[3] != 'G')
    {
        puts("ERROR: Invalid magic number!");
        exit(-1);
    }

    if (cimg.header.version != 2)
    {
        puts("ERROR: Unsupported version!");
        exit(-1);
    }

    initialize_framebuffer(&cimg);

    unsigned long data_size = cimg.header.width * cimg.header.height * sizeof(pixel_t);
    pixel_t *data = malloc(data_size);
    if (data == NULL)
    {
        puts("ERROR: Failed to allocate memory for the image data!");
        exit(-1);
    }
    read_exact(0, data, data_size, "ERROR: Failed to read data!", -1);

    for (int i = 0; i < cimg.header.width * cimg.header.height; i++)
    {
        if (data[i].ascii < 0x20 || data[i].ascii > 0x7e)
        {
            fprintf(stderr, "ERROR: Invalid character 0x%x in the image data!\n", data[i].ascii);
            exit(-1);
        }
    }

    display(&cimg, data);

    if (cimg.num_pixels != sizeof(desired_output)/sizeof(term_pixel_t))
    {
        won = 0;
    }
    for (int i = 0; i < cimg.num_pixels && i < sizeof(desired_output)/sizeof(term_pixel_t); i++)
    {
        if (cimg.framebuffer[i].str.c != ((term_pixel_t*)&desired_output)[i].str.c)
        {
            won = 0;
        }
        if (
            cimg.framebuffer[i].str.c != ' ' &&
            cimg.framebuffer[i].str.c != '\n' &&
            memcmp(cimg.framebuffer[i].data, ((term_pixel_t*)&desired_output)[i].data, sizeof(term_pixel_t))
        )
        {
            won = 0;
        }
    }

    if (won) win();

}
```


```
from pwn import *
import struct
import re

# Desired ANSI sequence
binary = context.binary = ELF('/challenge/cimg')
desired_ansi_sequence_bytes = binary.string(binary.sym.desired_output)
desired_ansi_sequence = desired_ansi_sequence_bytes.decode("utf-8")

# This regex looks for the RGB numbers and the character that follows the 'm'
# (\d+) matches the digits for R, G, and B
# m(.) matches the 'm' followed by the single character we want
pattern = r"\x1b\[38;2;(\d+);(\d+);(\d+)m(.)"

# Find all matches in the sequence
matches = re.findall(pattern, desired_ansi_sequence)

# Convert the strings to the format you want: (int, int, int, ord(char))
pixels = [
    (int(r), int(g), int(b), ord(char)) 
    for r, g, b, char in matches
]

pixel_data = b"".join(struct.pack("BBBB", r, g, b, a) for r, g, b, a in pixels)

width_value = 53
height_value = len(pixels) // width_value

# Build the header (8 bytes total)
magic = b"cIMG"                                 # 4 bytes
version = struct.pack("<H", 2)                  # 2 bytes
width  = struct.pack("<B", width_value)         # 1 bytes
height = struct.pack("<B", height_value)        # 1 bytes

header = magic + version + width + height

# Full file content
cimg_data = header + pixel_data

# Write to disk
filename = "/home/hacker/solution.cimg"
with open(filename, "wb") as f:
    f.write(cimg_data)

print(f"Wrote {len(cimg_data)} bytes: {cimg_data} to: {filename}")
```


```
from pwn import *
import struct
import re
import os

# Путь к бинарю и выходному файлу
BIN_PATH = "/challenge/cimg"
OUT_PATH = "/home/hacker/solution.cimg"

# Загружаем бинарь и достаём строку desired_output
binary = context.binary = ELF(BIN_PATH)
desired_ansi_sequence_bytes = binary.string(binary.sym.desired_output)
desired_ansi_sequence = desired_ansi_sequence_bytes.decode("utf-8")

# Регекс: ESC[38;2;R;G;BmX
pattern = r"\x1b

\[38;2;(\d+);(\d+);(\d+)m(.)"
matches = re.findall(pattern, desired_ansi_sequence)

# Превращаем в (R, G, B, ascii)
pixels = [
    (int(r), int(g), int(b), ord(ch))
    for r, g, b, ch in matches
]

# Собираем пиксельные данные: 4 байта на пиксель (R, G, B, A/ASCII)
pixel_data = b"".join(struct.pack("BBBB", r, g, b, a) for r, g, b, a in pixels)

# Можно оставить твою ширину, если она соответствует реальному арту
width_value = 53
height_value = len(pixels) // width_value

# Заголовок: "cIMG" + версия (2) + width + height
magic   = b"cIMG"              # 4 байта
version = struct.pack("<H", 2) # 2 байта
width   = struct.pack("<B", width_value)
height  = struct.pack("<B", height_value)

header = magic + version + width + height
cimg_data = header + pixel_data

os.makedirs(os.path.dirname(OUT_PATH), exist_ok=True)
with open(OUT_PATH, "wb") as f:
    f.write(cimg_data)

print(f"Wrote {len(cimg_data)} bytes to {OUT_PATH}")
```
