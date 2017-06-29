KSPDIR		:= ${HOME}/ksp/KSP_linux
MANAGED		:= ${KSPDIR}/KSP_Data/Managed
GAMEDATA	:= ${KSPDIR}/GameData
KSSGAMEDATA  := ${GAMEDATA}/KSCSwitcher
PLUGINDIR	:= ${KSSGAMEDATA}/Plugins

TARGETS		:= KSCSwitcher.dll

KSS_FILES := \
	CameraFixer.cs	\
	KSCLoader.cs	\
	KSCSwitcher.cs	\
	LastKSC.cs		\
	LaunchSite.cs	\
	Properties/AssemblyInfo.cs	\
	$e

DOC_FILES := \
	License.txt \
	README.md

RESGEN2		:= resgen2
GMCS		:= mcs
GMCSFLAGS	:= -optimize -warnaserror
GIT			:= git
TAR			:= tar
ZIP			:= zip

all: ${TARGETS} #KSCSwitcher.png

.PHONY: version
version:
	@./git-version.sh

info:
	@echo "KSCSwitcher Build Information"
	@echo "    resgen2:    ${RESGEN2}"
	@echo "    gmcs:       ${GMCS}"
	@echo "    gmcs flags: ${GMCSFLAGS}"
	@echo "    git:        ${GIT}"
	@echo "    tar:        ${TAR}"
	@echo "    zip:        ${ZIP}"
	@echo "    KSP Data:   ${KSPDIR}"

KSCSwitcher.dll: ${KSS_FILES}
	${GMCS} ${GMCSFLAGS} -t:library -lib:${MANAGED} \
		-r:Assembly-CSharp,Assembly-CSharp-firstpass \
		-r:UnityEngine,UnityEngine.UI \
		-out:$@ $^

KSCSwitcher.png: KSCSwitcher.svg
	inkscape --export-png $@ $^

clean:
	rm -f ${TARGETS} KSCSwitcher.png

install: all
	mkdir -p ${PLUGINDIR}
	cp ${TARGETS} ${PLUGINDIR}
#	cp ${DOC_FILES} ${KSSGAMEDATA}

.PHONY: all clean install
