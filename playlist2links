#!/bin/bash

if [[ -z "$1" ]];
then
	echo "Please, specify the playlist code as argument" 1>&2
	exit 1
fi
URL="https://www.youtube.com/playlist?list=$1"

TMPFILE=`mktemp /tmp/${tempfoo}.XXXXXX` || {
	echo "Temporary file creation failed" 1>&2
	exit 1
}

COMMAND=""
if [[ -n $(type -p wget) ]];
then
	COMMAND="wget -o /dev/null -O '${TMPFILE}.html' '$URL'"
fi
if [[ -z "$COMMAND" ]] && [[ -n $(type -p curl) ]];
then
	COMMAND="curl -s -o '${TMPFILE}.html' '$URL'"
fi
if [[ -z "$COMMAND" ]];
then
	echo "Please, install wget or curl to use this script" 1>&2
	exit 1
fi

eval $COMMAND
grep -e "^<tr.*<a href=\"/watch?v=.*$1" "${TMPFILE}.html" | sed 's/.*watch/https:\/\/www.youtube.com\/watch/g' | sed 's/&amp.*//g' > playlist_$1.txt

while [[ $(grep "continuation=" ${TMPFILE}.html) ]]
do
	sed -i 's/_continuation=1/\n/g' ${TMPFILE}.html
	CONTINUATION=$((sed 's/\(.*\)continuation=/https:\/\/www.youtube.com\/browse_ajax?action_continuation=1&/g' | sed 's/".*//g' | sed 's/\\u0026/\&/g' | tr -d '\' ) <<< $(grep "continuation=" ${TMPFILE}.html))
	
	if [[ -n $(type -p wget) ]];
	then
		wget -o /dev/null -O "${TMPFILE}.html" "$CONTINUATION"
	else
		curl -s -o "${TMPFILE}.html" "$CONTINUATION"
	fi

	tr -s '\\|/' '\n' < ${TMPFILE}.html >  "${TMPFILE}"
	grep "^watch" ${TMPFILE} | sed 's/\\u0026amp;\(.*\)//g' | sed 's/watch/https:\/\/www.youtube.com\/watch/g' | sort -u >> playlist_$1.txt
done

rm -f ${TMPFILE}*
