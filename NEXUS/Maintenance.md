# NEXUS MAINTENANCE


## WORKING WITH API

### DOWNLOAD


1 file

```
NEXUS_E2E_USER="usr"
NEXUS_E2E_PWD="pwd"
NEXUS_URL="https://nexus.tools.devopenocean.studio"
REPO="raw"
REPO_DIR="to_del_remotelyuploaded"
FILE_NAME="index.html"

wget --auth-no-challenge --user ${NEXUS_E2E_USER} --password  ${NEXUS_E2E_PWD} ${NEXUS_URL}/repository/${REPO}/${REPO_DIR}/${FILE_NAME}
```

Multiply files

```
NEXUS_E2E_USER="usr"
NEXUS_E2E_PWD="pwd"
NEXUS_URL="https://nexus.tools.devopenocean.studio"
REPO="raw"
REPO_DIR="to_del_remotelyuploaded"
FILE_LIST="/tmp/file_list.txt"

curl -X GET -u ${NEXUS_E2E_USER}:${NEXUS_E2E_PWD} ${NEXUS_URL}/service/rest/v1/search/assets | grep ${REPO} | grep ${REPO_DIR} > ${FILE_LIST}

for file in `cat ${FILE_LIST} | sed 's/.*: "//' | sed 's/",.*//'`
do
   wget --recursive --auth-no-challenge --user ${NEXUS_E2E_USER} --password  ${NEXUS_E2E_PWD} $file
done
```


### UPLOAD


1 file

```
NEXUS_E2E_USER="usr"
NEXUS_E2E_PWD="pwd"
NEXUS_URL="https://nexus.tools.devopenocean.studio"
REPO="raw"
REPO_DIR="to_del_temp"
DIR_WITH_FILE="/Users/sbur/overall/git_area/to_del/s3-static-website/uploaded/crewing"
FILE_NAME="crewing.tar.gz"

cd ${DIR_WITH_FILE}
curl -v -u ${NEXUS_E2E_USER}:${NEXUS_E2E_PWD} --upload-file ${FILE_NAME} ${NEXUS_URL}/repository/${REPO}/${REPO_DIR}/${FILE_NAME}
```


Multiply files

```
NEXUS_E2E_USER="usr"
NEXUS_E2E_PWD="pwd"
NEXUS_URL="https://nexus.tools.devopenocean.studio"
REPO="raw"
REPO_DIR="to_del_temp"
DIR_TO_UPLOAD="/Users/sbur/overall/git_area/to_del/s3-static-website/should_be_on_nexus"

cd ${DIR_TO_UPLOAD}
find . -type f -exec curl --user ${NEXUS_E2E_USER}:${NEXUS_E2E_PWD} --ftp-create-dirs -T {} ${NEXUS_URL}/repository/${REPO}/${REPO_DIR}/{} \;
```
