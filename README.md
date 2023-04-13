# _ReconGuasu_

# _Pequeño script basico para enumerar subdominio_

    #!/bin/bash

    #Autor= "Nu||d3v"

    #Automatization for Search subdomaind === "amass","assetfinder","findomain","subfinder","sublist3r","crobat","turbolist3r.py","ctfr.py","anubis","acamar.py","github-subdomains.oy","shuffledns","cencys-subdomain.py"

    dominio=$1
    resolvers=/home/josema96/HackerOne/hunters_tools/resolvers.txt
    permu=/home/josema96/mi_metodologia/Script_reconFORsubdomain/permutations.txtt

    #funtion1
    Help(){
      echo -e "\n\tRcon_Scriptkiddie.sh"
      echo -e "\n\tEjemplo de ejecución de la herramienta"
      echo -e "\n\t./subLyJ.sh"
    }

    #funtion2
    vali_domain(){
      host $dominio > /dev/null 2>&1
    }

    #funtion3
    subdomain(){
      mkdir -p $dominio $dominio/sub

      #echo -e "\n\tsearch subdomains con 'amass\n'";
      #amass enum -d $dominio | sort -u | anew $dominio/sub/amass.txt;
      #echo -e "\ntermino la ejecution 'amass'\n";
      echo -e "\n\tsearch subdomains con 'assetfinder'\n";
      assetfinder --subs-only $dominio | sort -u | anew $dominio/sub/asset.txt;
      echo -e "\n\ttermino la ejecution con 'assetfinder'\n";
      echo -e "\n\tsearch subdomains con 'findomain'\n";
      findomain --output -t $dominio 2> /dev/null ; cp $(pwd)/*.txt $dominio/sub ; rm $(pwd)/*.txt;
      #findomain -t $dominio | sort -u | anew $dominio/sub/findo.txt;
      echo -e "\n\ttermino la ejecution con 'findomain'\n";
      echo -e "\n\tsearch subdomains con 'subfinder'\n";
      subfinder -d $dominio | sort -u | anew $dominio/sub/subfin.txt;
      echo -e "\n\ttermino la ejecution con 'subfinder'\n";
      echo -e "\n\tsearch subdomains con 'sublist3r'\n";
      sublist3r -d $dominio -o $dominio/sub/sublis.txt;
      echo -e "\n\ttermino la ejecution con 'sublist3r'\n";
      echo -e "\n\tsearch subdomains con 'crobat'\n";
      crobat -s $dominio | sort -u | anew $dominio/sub/crob.txt;
      echo -e "\n\ttermino la ejecution con 'crobat'\n";
      echo -e "\n\tsearch subdomains con 'turbolist3r'\n";
      turbolist3r.py -d $dominio -o $dominio/sub/turbo.txt;
      echo -e "\n\ttermino la ejecution con 'turbolist3r'\n";
      echo -e "\n\tsearch subdomains con 'ctfr.py'\n";
      ctfr.py -d $dominio -o $dominio/sub/ctfr.txt;
      echo -e "\n\ttermino la ejecution con 'ctfr.py'\n";
      echo -e "\n\tsearch subdomains con 'anubis'\n";
      anubis -t $dominio  -S | sort -u | anew $dominio/sub/anub.txt;
      echo -e "\n\ttermino la ejecution con 'anubis'\n";
      #echo -e "\n\tsearch subdomains con 'github-subdomains.py'\n";
      #github-subdomains.py -t ghp_bSlKa.... -d $dominio | sort -u | anew $dominio/sub/git_su.txt;
      #echo -e "\n\ttermino la ejecution con 'github-subdomains.py'\n";
      #echo -e "\n\tsearch subdomains con 'cencys-subdomain.py'\n";
      #censys-subdomain.py --censys-api-id 00d-3bf-04-a75f-8f1 --censys-api-secret rxDx5UEfrC...  $dominio | sort -u | anew $dominio/sub/cen_sub.txt;
      #echo -e "\n\ttermino la ejecution con 'cencys-subdomain.py'\n";
      echo -e "\n\tguardando todo los sub all 'allSub'\n"

    }

    ############################################################################################
    #Ejecución de puredns:

    puredns(){
      echo -e "\n\tsearch subdominio con Puredns\n"
      puredns bruteforce $wordlists $dominio -r $resolvers -w $dominio/sub/bruteSub.txt
      #xargs -a $dominio/sub/bruteSub.txt -I@ sh -c 'subfinder -d @ | anew $dominio/sub/xargs.txt'
      echo -e "\n\ttermno la ejecucion de BruteForce con puredns\n"
    }

    ################################################################################################
    #GOOGLE ANALITIC con "BuiltWidth" es una extension
    #Utilizamos una tools en lineas de comando llamado "AnaliticsRelationships"

    AnaliticsRelationships(){

      echo -e "\n\tSearch sundominio con Analyticsrelationships\n"
      analyticsrelationships --url $dominio | anew $dominio/sub/analytic.txt
      cat $dominio/sub/analytic.txt  | awk '{print $2}' | grep '.hackerone.com' | anew  $domain/sub/analitics.txt
      rm  $domain/sub/analytic.txt
      echo -e "\n\ttermno la ejecucion de AnaliticsRelationships\n"

    #analyticsrelationships -u hackerone.com > tests ; cat tests | awk '{print $2}' | grep "hackerone.com"
    }

    ################################################################################################
    #Premutation/Alterations

    permuALTe(){

      cp $domain/sub/*.txt $domain/sub/suball
      echo -e "\n\tsearch posible subdominio con Gotator usando todos los subdominio encontardo\n"
      gotator -sub $domain/sub/suball -perm $permu -depth 1 -numbers 10 -mindup -adv -md | anew $dominio/sub/permuSub.txt
      rm $domain/sub/suball
      echo -e "\n\ttermno la ejecucion de Gotator\n"

    _De forma directa ejecuando assetfinder_
    #echo [+] ejecuando assetfinder ; assetfinder -subs-only testphp.vulnweb.com | tee sub.txt ; gotator -sub sub.txt -perm permutations.txtt -depth 1 -numbers 10 -mindup -adv -md > perm.txt ; puredns resolve perm.txt -r resolvers.txt | anew valido.tx

    #otra manera de resolver o validar dns
    #assetfinder -subs-only testphp.vulnweb.com | tail -6 | massdns -r resolvers.txt -t A -o S -w resul.txt.
    }

    ###########################################################################################

    #1)Subdomio de Sondeo Web

    js_code_Sub(){

      cp $dominio/sub/*.txt $dominio/sub/allSub
      echo -e "\n\tsearch posible subdominio con httpx y gospider\n"

    #Scraping(JS/source code) o raspado(JS/codigo fuente)
    #corrindo gospider ====> Este proseso se divide en tres parte
    #1)Subdomio de Sondeo Web
    #2)Limpiesa de Salida
    #3)Resolver nuestro dominio del destino

    #1)Subdomio de Sondeo Web
      cat $dominio/sub/allSub | httpx -random-agent -retries 2 -no-color | anew $dominio/sub/urlpro.txt
    #-S, --sites | -t, --threads | #-w, --include-subs | -d, --depth | -r, --include-other-source
      gospider -S $dominio/sub/urlpro.txt --js -t 50 -d 3 --sitemap --robots -w -r | anew  $dominio/sub/gos_js.txt
    #2)Limpiesa de Salida
      cat $dominio/sub/gos_js.txt | sed '/^.\{2048\}./d' > $dominio/sub/gosprob.txt;
      $dominio/sub/gosprob.txt | grep -Eo 'https?://[^ ]+' | sed 's/]$//' | unfurl -u domains | grep 'hackerone.com' | sort - u | anew $dominio/sub/gospiJScodeSub.txt
      rm $dominio/sub/urlpro.txt $dominio/sub/gos_js.txt $dominio/sub/gosprob.txt $dominio/sub/allSub

    #echo [+] ejecutando assetfinder [+] ; echo "testphp.vulnweb.com" | assetfinder -subs-only |  tee sub.txt1 ; cat sub.txt1 ; httpx -silent -random-agent -retries 2 -no-color | tee http.txt2 ; gospider -S http.txt2 --js -t 50 -d 1 --sitemap --robots -w -r | tail -1000 | anew gos.txt3 ; cat gos.txt3 | grep -Eo 'https?://[^ ]+' | sed 's/]$//' | unfurl -u domains | anew subvalido.txt4

    #echo [+] ejecutando assetfinder [+] ; echo "testphp.vulnweb.com" | assetfinder -subs-only > sub.txt1 ; cat sub.txt1 ; httpx -silent -random-agent -retries 2 -no-color > http.txt2 ; gospider -S http.txt2 --js -t 50 -d 1 --sitemap --robots -w -r > gos.txt3 ; cat gos.txt3 | grep -Eo 'https?://[^ ]+' | sed 's/]$//' | unfurl -u domains | anew subvalido.txt4

    }

    ###################################################################################################

    xargsSub(){
      cp $dominio/sub/*.txt $dominio/sub/xargsSub
      echo -e "\n\tSearch buscando subdominio dentro de subdominio Encontrado'\n"
            xargs -a $dominio/sub/xargsSub -I@ sh -c 'subfinder -d @ -silent | anew $dominio/sub/xargs.txt'
      echo -e "\n\tTermino la ejecucion con xargs'\n"
      rm $dominio/sub/xargsSub

    }

    resol_Domain(){
      cp $dominio/sub/*.txt $dominio/sub/resolverSub
      #echo -e "\n\tValidando resolvers DNS con 'puredns'\n"
      #puredns resolve $dominio/sub/resolverSub -w $domain/sub/sub_real.txt -r $resolvers
      #echo -e "\n\tsubdomain validando con exito con 'puredns'\n"
      #xargs -a $dominio/sub/allsub -I@ sh -c 'puredns resolve @ -w $domain/sub/sub_real.txt -r $resolvers'

    #}


    #funtion8
    #main call funtions
    if [ "$#" == "1" ];then
      vali_domain
      if [ "$(echo $?)" == "0" ];then
        subdomain
        puredns
        AnaliticsRelationships
        permuALTe
        js_code_Sub
        xargsSub
        resol_Domain
      else
        echo -e "\nno es un dominio"
      fi
    else
      Help

    fi

