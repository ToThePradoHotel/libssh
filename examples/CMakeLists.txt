project(libssh-examples C CXX)

set(examples_SRCS
  authentication.c
  knownhosts.c
  connect_ssh.c
)

include_directories(
  ${LIBSSH_PUBLIC_INCLUDE_DIRS}
  ${CMAKE_BINARY_DIR}
)

if (LINUX)
    add_executable(libssh_scp libssh_scp.c ${examples_SRCS})
    target_link_libraries(libssh_scp ${LIBSSH_SHARED_LIBRARY})

    add_executable(scp_download scp_download.c ${examples_SRCS})
    target_link_libraries(scp_download ${LIBSSH_SHARED_LIBRARY})

    add_executable(samplessh sample.c ${examples_SRCS})
    target_link_libraries(samplessh ${LIBSSH_SHARED_LIBRARY})

    add_executable(sshnetcat sshnetcat.c ${examples_SRCS})
    target_link_libraries(sshnetcat ${LIBSSH_SHARED_LIBRARY})

    if (WITH_SFTP)
        add_executable(samplesftp samplesftp.c ${examples_SRCS})
        target_link_libraries(samplesftp ${LIBSSH_SHARED_LIBRARY})
    endif (WITH_SFTP)

    if (WITH_SERVER)
        add_executable(samplesshd samplesshd.c)
        target_link_libraries(samplesshd ${LIBSSH_SHARED_LIBRARY})

        add_executable(samplesshd-kbdint samplesshd-kbdint.c)
        target_link_libraries(samplesshd-kbdint ${LIBSSH_SHARED_LIBRARY})

        if (HAVE_LIBUTIL)
            add_executable(samplesshd-tty samplesshd-tty.c)
            target_link_libraries(samplesshd-tty ${LIBSSH_SHARED_LIBRARY} util)
        endif (HAVE_LIBUTIL)

    endif (WITH_SERVER)
endif (LINUX)

add_executable(exec exec.c ${examples_SRCS})
target_link_libraries(exec ${LIBSSH_SHARED_LIBRARY})

add_executable(senddata senddata.c ${examples_SRCS})
target_link_libraries(senddata ${LIBSSH_SHARED_LIBRARY})

add_executable(libsshpp libsshpp.cpp)
target_link_libraries(libsshpp ${LIBSSH_SHARED_LIBRARY})

add_executable(libsshpp_noexcept libsshpp_noexcept.cpp)
target_link_libraries(libsshpp_noexcept ${LIBSSH_SHARED_LIBRARY})
