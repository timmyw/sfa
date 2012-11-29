project(sfa)

set(SRCS
  sfalib.cpp)

addlib(sfa SHARED "${SRCS}" "")

FILE(GLOB incfiles "${MAIN_INC_DIR}/*.[hi]")
install(FILES ${incfiles} DESTINATION ${incdir}/ballista)
