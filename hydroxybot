#!/bin/bash


_get_repolink () {
    local regex
    regex='(https?)://github.com/.+/.+'
    if [[ $HYDROXY_REPO == "hydroxybot" ]]
    then
        echo "aHR0cHM6Ly9naXRodWIuY29tL0gxTTRONUhVMFAvTUFGSUEtVVNFUkJPVC9hcmNoaXZlL21hc3Rlci56aXA=" | base64 -d
    elif [[ $HYDROXY_REPO == "HYDROXYBOT" ]]
    then
        echo "aHR0cHM6Ly9naXRodWIuY29tL0gxTTRONUhVMFAvTUFGSUEtVVNFUkJPVC9hcmNoaXZlL21hc3Rlci56aXA=" | base64 -d
    elif [[ $HYDROXY_REPO =~ $regex ]]
    then
        if [[ $HYDROXY_REPO_BRANCH ]]
        then
            echo "${HYDROXY_REPO}/archive/${HYDROXY_REPO_BRANCH}.zip"
        else
            echo "${HYDROXY_REPO}/archive/master.zip"
        fi
    else
        echo "aHR0cHM6Ly9naXRodWIuY29tL0gxTTRONUhVMFAvTUFGSUEtVVNFUkJPVC9hcmNoaXZlL21hc3Rlci56aXA=" | base64 -d
    fi
}


_set_bot () {
    local zippath
    zippath="hydroxybot.zip"
    echo "  Downloading source code ..."
    wget -q $(_get_repolink) -O "$zippath"
    echo "  Unpacking Data ..."
    HYDROXYPATH=$(zipinfo -1 "$zippath" | grep -v "/.");
    unzip -qq "$zippath"
    echo "Done"
    echo "  Cleaning ..."
    rm -rf "$zippath"
    sleep 5
    cd $HYDROXYPATH
    echo "    Starting hydroxyBot    "
    echo "
                          ╔═╦═╦══╦══╦══╦══╦══╦═╦══╗
                          ║║║║║╔╗║═╦╩║║╣╔╗║╔╗║║╠╗╔╝
                          ║║║║║╠╣║╔╝╔║║╣╠╣║╔╗║║║║║
                          ╚╩═╩╩╝╚╩╝─╚══╩╝╚╩══╩═╝╚╝
    "

    python3 ./setup/updater.py ./requirements.txt requirements.txt
    python3 -m userbot
}

_set_bot
