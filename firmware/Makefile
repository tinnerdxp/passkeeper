STRIP=-ldflags '-s -w'
TOS ?= linux
TARCH ?= arm

OSBUILD=GOOS=${TOS} GOARCH=${TARCH} CGOENABLED=0
OUT=../buildroot/board/rootfs_overlay/root
EXECS=service util splash

PHONY: packr packr-dep

all: packr upx

packr: packr-dep
	packr

${OUT}/service:
	${OSBUILD} go build ${STRIP} -o ${OUT}/service app/service/*.go

${OUT}/util:
	${OSBUILD} go build ${STRIP} -o ${OUT}/util app/util/*.go

${OUT}/splash:
	${OSBUILD} go build ${STRIP} -o ${OUT}/splash app/splash/*.go

packr-dep:
	go get -u github.com/gobuffalo/packr/packr

upx: ${OUT}/service ${OUT}/util ${OUT}/splash
	upx ${OUT}/service
	upx ${OUT}/util
	upx ${OUT}/splash

clean: packr-dep
	packr clean
	rm -f $(addprefix $(OUT)/, $(EXECS))
