> 本文内容由[模块:EFloras](https://zh.wikipedia.org/wiki/模块:EFloras)转换而来。


require('Module:No globals')

local p = {}

local volumeTable = {

`   ["Flora of North America"] = {`
`       ["Anemiaceae"] = "2",`
`       ["Aspleniaceae"] = "2",`
`       ["Azollaceae"] = "2",`
`       ["Blechnaceae"] = "2",`
`       ["Cupressaceae"] = "2",`
`       ["Dennstaedtiaceae"] = "2",`
`       ["Dryopteridaceae"] = "2",`
`       ["Ephedraceae"] = "2",`
`       ["Equisetaceae"] = "2",`
`       ["Ginkgoaceae"] = "2",`
`       ["Gleicheniaceae"] = "2",`
`       ["Grammitidaceae"] = "2",`
`       ["Hymenophyllaceae"] = "2",`
`       ["Isoëtaceae"] = "2",`
`       ["Lycopodiaceae"] = "2",`
`       ["Lygodiaceae"] = "2",`
`       ["Marsileaceae"] = "2",`
`       ["Ophioglossaceae"] = "2",`
`       ["Osmundaceae"] = "2",`
`       ["Parkeriaceae"] = "2",`
`       ["Pinaceae"] = "2",`
`       ["Polypodiaceae"] = "2",`
`       ["Psilotaceae"] = "2",`
`       ["Pteridaceae"] = "2",`
`       ["Salviniaceae"] = "2",`
`       ["Schizaeaceae"] = "2",`
`       ["Selaginellaceae"] = "2",`
`       ["Taxaceae"] = "2",`
`       ["Thelypteridaceae"] = "2",`
`       ["Vittariaceae"] = "2",`
`       ["Zamiaceae"] = "2",`
`       ["Annonaceae"] = "3",`
`       ["Aristolochiaceae"] = "3",`
`       ["Berberidaceae"] = "3",`
`       ["Betulaceae"] = "3",`
`       ["Cabombaceae"] = "3",`
`       ["Calycanthaceae"] = "3",`
`       ["Canellaceae"] = "3",`
`       ["Cannabaceae"] = "3",`
`       ["Casuarinaceae"] = "3",`
`       ["Ceratophyllaceae"] = "3",`
`       ["Fagaceae"] = "3",`
`       ["Fumariaceae"] = "3",`
`       ["Hamamelidaceae"] = "3",`
`       ["Illiciaceae"] = "3",`
`       ["Juglandaceae"] = "3",`
`       ["Lardizabalaceae"] = "3",`
`       ["Lauraceae"] = "3",`
`       ["Leitneriaceae"] = "3",`
`       ["Magnoliaceae"] = "3",`
`       ["Menispermaceae"] = "3",`
`       ["Moraceae"] = "3",`
`       ["Myricaceae"] = "3",`
`       ["Nelumbonaceae"] = "3",`
`       ["Nymphaeaceae"] = "3",`
`       ["Papaveraceae"] = "3",`
`       ["Piperaceae"] = "3",`
`       ["Platanaceae"] = "3",`
`       ["Ranunculaceae"] = "3",`
`       ["Saururaceae"] = "3",`
`       ["Schisandraceae"] = "3",`
`       ["Ulmaceae"] = "3",`
`       ["Urticaceae"] = "3",`
`       ["Achatocarpaceae"] = "4",`
`       ["Aizoaceae"] = "4",`
`       ["Amaranthaceae"] = "4",`
`       ["Basellaceae"] = "4",`
`       ["Cactaceae"] = "4",`
`       ["Chenopodiaceae"] = "4",`
`       ["Molluginaceae"] = "4",`
`       ["Nyctaginaceae"] = "4",`
`       ["Phytolaccaceae"] = "4",`
`       ["Portulacaceae"] = "4",`
`       ["Caryophyllaceae"] = "5",`
`       ["Plumbaginaceae"] = "5",`
`       ["Polygonaceae"] = "5",`
`       ["Apodanthaceae"] = "6",`
`       ["Begoniaceae"] = "6",`
`       ["Calophyllaceae"] = "6",`
`       ["Cistaceae"] = "6",`
`       ["Clusiaceae"] = "6",`
`       ["Cochlospermaceae"] = "6",`
`       ["Cucurbitaceae"] = "6",`
`       ["Datiscaceae"] = "6",`
`       ["Droseraceae"] = "6",`
`       ["Frankeniaceae"] = "6",`
`       ["Hypericaceae"] = "6",`
`       ["Malvaceae"] = "6",`
`       ["Muntingiaceae"] = "6",`
`       ["Passifloraceae"] = "6",`
`       ["Podostemaceae"] = "6",`
`       ["Tamaricaceae"] = "6",`
`       ["Thymelaeaceae"] = "6",`
`       ["Turneraceae"] = "6",`
`       ["Violaceae"] = "6",`
`       ["Bataceae"] = "7",`
`       ["Brassicaceae"] = "7",`
`       ["Capparaceae"] = "7",`
`       ["Caricaceae"] = "7",`
`       ["Cleomaceae"] = "7",`
`       ["Koeberliniaceae"] = "7",`
`       ["Limnanthaceae"] = "7",`
`       ["Moringaceae"] = "7",`
`       ["Resedaceae"] = "7",`
`       ["Salicaceae"] = "7",`
`       ["Tropaeolaceae"] = "7",`
`       ["Clethraceae"] = "8",`
`       ["Crassulaceae"] = "8",`
`       ["Cyrillaceae"] = "8",`
`       ["Diapensiaceae"] = "8",`
`       ["Ebenaceae"] = "8",`
`       ["Ericaceae"] = "8",`
`       ["Grossulariaceae"] = "8",`
`       ["Iteaceae"] = "8",`
`       ["Myrsinaceae"] = "8",`
`       ["Paeoniaceae"] = "8",`
`       ["Penthoraceae"] = "8",`
`       ["Primulaceae"] = "8",`
`       ["Sapotaceae"] = "8",`
`       ["Sarraceniaceae"] = "8",`
`       ["Saxifragaceae"] = "8",`
`       ["Styracaceae"] = "8",`
`       ["Symplocaceae"] = "8",`
`       ["Theaceae"] = "8",`
`       ["Theophrastaceae"] = "8",`
`       ["Crossosomataceae"] = "9",`
`       ["Picramniaceae"] = "9",`
`       ["Rosaceae"] = "9",`
`       ["Staphyleaceae"] = "9",`

\-- The following names in volumes 19-21 are tribes of the family Asteraceae.

`       ["Cichorieae"] = "19",`
`       ["Arctotideae"] = "19",`
`       ["Anthemideae"] = "19",`
`       ["Vernonieae"] = "19",`
`       ["Mutisieae"] = "19",`
`       ["Cardueae"] = "19",`
`       ["Calenduleae"] = "19",`
`       ["Inuleae"] = "19",`
`       ["Gnaphalieae"] = "19",`
`       ["Plucheeae"] = "19",`
`       ["Asteraceae"] = "error",`
`       ["Astereae"] = "20",`
`       ["Senecioneae"] = "20",`
`       ["Eupatorieae"] = "21",`
`       ["Heliantheae"] = "21",`

\-- end of list of tribes of Asteraceae

`       ["Acoraceae"] = "22",`
`       ["Alismataceae"] = "22",`
`       ["Aponogetonaceae"] = "22",`
`       ["Araceae"] = "22",`
`       ["Arecaceae"] = "22",`
`       ["Bromeliaceae"] = "22",`
`       ["Butomaceae"] = "22",`
`       ["Cannaceae"] = "22",`
`       ["Commelinaceae"] = "22",`
`       ["Cymodoceaceae"] = "22",`
`       ["Eriocaulaceae"] = "22",`
`       ["Heliconiaceae"] = "22",`
`       ["Hydrocharitaceae"] = "22",`
`       ["Juncaceae"] = "22",`
`       ["Juncaginaceae"] = "22",`
`       ["Lemnaceae"] = "22",`
`       ["Limnocharitaceae"] = "22",`
`       ["Marantaceae"] = "22",`
`       ["Mayacaceae"] = "22",`
`       ["Musaceae"] = "22",`
`       ["Najadaceae"] = "22",`
`       ["Potamogetonaceae"] = "22",`
`       ["Ruppiaceae"] = "22",`
`       ["Scheuchzeriaceae"] = "22",`
`       ["Sparganiaceae"] = "22",`
`       ["Typhaceae"] = "22",`
`       ["Xyridaceae"] = "22",`
`       ["Zannichelliaceae"] = "22",`
`       ["Zingiberaceae"] = "22",`
`       ["Zosteraceae"] = "22",`
`       ["Cyperaceae"] = "23",`
`       ["Agavaceae"] = "26",`
`       ["Aloaceae"] = "26",`
`       ["Burmanniaceae"] = "26",`
`       ["Dioscoreaceae"] = "26",`
`       ["Haemodoraceae"] = "26",`
`       ["Iridaceae"] = "26",`
`       ["Liliaceae"] = "26",`
`       ["Orchidaceae"] = "26",`
`       ["Pontederiaceae"] = "26",`
`       ["Smilacaceae"] = "26",`
`       ["Stemonaceae"] = "26",`
`       ["Andreaeaceae"] = "27",`
`       ["Andreaeobryaceae"] = "27",`
`       ["Archidiaceae"] = "27",`
`       ["Bruchiaceae"] = "27",`
`       ["Bryoxiphiaceae"] = "27",`
`       ["Buxbaumiaceae"] = "27",`
`       ["Calymperaceae"] = "27",`
`       ["Dicranaceae"] = "27",`
`       ["Diphysciaceae"] = "27",`
`       ["Disceliaceae"] = "27",`
`       ["Ditrichaceae"] = "27",`
`       ["Encalyptaceae"] = "27",`
`       ["Ephemeraceae"] = "27",`
`       ["Erpodiaceae"] = "27",`
`       ["Fissidentaceae"] = "27",`
`       ["Funariaceae"] = "27",`
`       ["Gigaspermaceae"] = "27",`
`       ["Grimmiaceae"] = "27",`
`       ["Leucobryaceae"] = "27",`
`       ["Leucophanaceae"] = "27",`
`       ["Oedipodiaceae"] = "27",`
`       ["Polytrichaceae"] = "27",`
`       ["Pottiaceae"] = "27",`
`       ["Ptychomitriaceae"] = "27",`
`       ["Rhachitheciaceae"] = "27",`
`       ["Schistostegaceae"] = "27",`
`       ["Scouleriaceae"] = "27",`
`       ["Seligeriaceae"] = "27",`
`       ["Sphagnaceae"] = "27",`
`       ["Splachnobryaceae"] = "27",`
`       ["Takakiaceae"] = "27",`
`       ["Tetraphidaceae"] = "27",`
`       ["Timmiaceae"] = "27",`
`       ["Amblystegiaceae"] = "28",`
`       ["Anomodontaceae"] = "28",`
`       ["Aulacomniaceae"] = "28",`
`       ["Bartramiaceae"] = "28",`
`       ["Brachytheciaceae"] = "28",`
`       ["Bryaceae"] = "28",`
`       ["Calliergonaceae"] = "28",`
`       ["Catoscopiaceae"] = "28",`
`       ["Climaciaceae"] = "28",`
`       ["Cryphaeaceae"] = "28",`
`       ["Daltoniaceae"] = "28",`
`       ["Entodontaceae"] = "28",`
`       ["Fabroniaceae"] = "28",`
`       ["Fontinalaceae"] = "28",`
`       ["Hedwigiaceae"] = "28",`
`       ["Helodiaceae"] = "28",`
`       ["Hookeriaceae"] = "28",`
`       ["Hylocomiaceae"] = "28",`
`       ["Hypnaceae"] = "28",`
`       ["Hypopterygiaceae"] = "28",`
`       ["Lembophyllaceae"] = "28",`
`       ["Leptodontaceae"] = "28",`
`       ["Leskeaceae"] = "28",`
`       ["Leucodontaceae"] = "28",`
`       ["Meesiaceae"] = "28",`
`       ["Meteoriaceae"] = "28",`
`       ["Mielichhoferiaceae"] = "28",`
`       ["Mniaceae"] = "28",`
`       ["Myriniaceae"] = "28",`
`       ["Neckeraceae"] = "28",`
`       ["Orthodontiaceae"] = "28",`
`       ["Orthotrichaceae"] = "28",`
`       ["Pilotrichaceae"] = "28",`
`       ["Plagiotheciaceae"] = "28",`
`       ["Pleuroziopsaceae"] = "28",`
`       ["Pseudoditrichaceae"] = "28",`
`       ["Pterigynandraceae"] = "28",`
`       ["Pterobryaceae"] = "28",`
`       ["Racopilaceae"] = "28",`
`       ["Rhizogoniaceae"] = "28",`
`       ["Rhytidiaceae"] = "28",`
`       ["Roellobryaceae"] = "28",`
`       ["Rutenbergiaceae"] = "28",`
`       ["Sematophyllaceae"] = "28",`
`       ["Splachnaceae"] = "28",`
`       ["Stereophyllaceae"] = "28",`
`       ["Theliaceae"] = "28",`
`       ["Thuidiaceae"] = "28",`
`       },`
`   ["Flora of China"] = {`
`       ["Aspleniaceae"] = "2",`
`       ["Athyriaceae"] = "2",`
`       ["Blechnaceae"] = "2",`
`       ["Cibotiaceae"] = "2",`
`       ["Cyatheaceae"] = "2",`
`       ["Cystopteridaceae"] = "2",`
`       ["Davalliaceae"] = "2",`
`       ["Dennstaedtiaceae"] = "2",`
`       ["Diplaziopsidaceae"] = "2",`
`       ["Dipteridaceae"] = "2",`
`       ["Dryopteridaceae"] = "2",`
`       ["Equisetaceae"] = "2",`
`       ["Gleicheniaceae"] = "2",`
`       ["Hymenophyllaceae"] = "2",`
`       ["Hypodematiaceae"] = "2",`
`       ["Isoetaceae"] = "2",`
`       ["Isoëtaceae"] = "2",`
`       ["Lindsaeaceae"] = "2",`
`       ["Lomariopsidaceae"] = "2",`
`       ["Lycopodiaceae"] = "2",`
`       ["Lygodiaceae"] = "2",`
`       ["Marattiaceae"] = "2",`
`       ["Marsileaceae"] = "2",`
`       ["Nephrolepidaceae"] = "2",`
`       ["Oleandraceae"] = "2",`
`       ["Onocleaceae"] = "2",`
`       ["Ophioglossaceae"] = "2",`
`       ["Osmundaceae"] = "2",`
`       ["Plagiogyriaceae"] = "2",`
`       ["Polypodiaceae"] = "2",`
`       ["Psilotaceae"] = "2",`
`       ["Pteridaceae"] = "2",`
`       ["Rhachidosoraceae"] = "2",`
`       ["Salviniaceae"] = "2",`
`       ["Schizaeaceae"] = "2",`
`       ["Selaginellaceae"] = "2",`
`       ["Tectariaceae"] = "2",`
`       ["Thelypteridaceae"] = "2",`
`       ["Woodsiaceae"] = "2",`
`       ["Araucariaceae"] = "4",`
`       ["Betulaceae"] = "4",`
`       ["Casuarinaceae"] = "4",`
`       ["Cephalotaxaceae"] = "4",`
`       ["Chloranthaceae"] = "4",`
`       ["Cupressaceae"] = "4",`
`       ["Cycadaceae"] = "4",`
`       ["Ephedraceae"] = "4",`
`       ["Fagaceae"] = "4",`
`       ["Ginkgoaceae"] = "4",`
`       ["Gnetaceae"] = "4",`
`       ["Juglandaceae"] = "4",`
`       ["Myricaceae"] = "4",`
`       ["Pinaceae"] = "4",`
`       ["Piperaceae"] = "4",`
`       ["Podocarpaceae"] = "4",`
`       ["Salicaceae"] = "4",`
`       ["Saururaceae"] = "4",`
`       ["Sciadopityaceae"] = "4",`
`       ["Taxaceae"] = "4",`
`       ["Taxodiaceae"] = "4",`
`       ["Aizoaceae"] = "5",`
`       ["Amaranthaceae"] = "5",`
`       ["Aristolochiaceae"] = "5",`
`       ["Balanophoraceae"] = "5",`
`       ["Basellaceae"] = "5",`
`       ["Cannabaceae"] = "5",`
`       ["Chenopodiaceae"] = "5",`
`       ["Loranthaceae"] = "5",`
`       ["Molluginaceae"] = "5",`
`       ["Moraceae"] = "5",`
`       ["Nyctaginaceae"] = "5",`
`       ["Olacaceae"] = "5",`
`       ["Opiliaceae"] = "5",`
`       ["Phytolaccaceae"] = "5",`
`       ["Podostemaceae"] = "5",`
`       ["Polygonaceae"] = "5",`
`       ["Portulacaceae"] = "5",`
`       ["Proteaceae"] = "5",`
`       ["Rafflesiaceae"] = "5",`
`       ["Rhoipteleaceae"] = "5",`
`       ["Santalaceae"] = "5",`
`       ["Ulmaceae"] = "5",`
`       ["Urticaceae"] = "5",`
`       ["Viscaceae"] = "5",`
`       ["Cabombaceae"] = "6",`
`       ["Caryophyllaceae"] = "6",`
`       ["Ceratophyllaceae"] = "6",`
`       ["Cercidiphyllaceae"] = "6",`
`       ["Circaeasteraceae"] = "6",`
`       ["Eupteleaceae"] = "6",`
`       ["Lardizabalaceae"] = "6",`
`       ["Nelumbonaceae"] = "6",`
`       ["Nymphaeaceae"] = "6",`
`       ["Paeoniaceae"] = "6",`
`       ["Ranunculaceae"] = "6",`
`       ["Tetracentraceae"] = "6",`
`       ["Trochodendraceae"] = "6",`
`       ["Calycanthaceae"] = "7",`
`       ["Capparaceae"] = "7",`
`       ["Cleomaceae"] = "7",`
`       ["Hernandiaceae"] = "7",`
`       ["Illiciaceae"] = "7",`
`       ["Lauraceae"] = "7",`
`       ["Magnoliaceae"] = "7",`
`       ["Menispermaceae"] = "7",`
`       ["Myristicaceae"] = "7",`
`       ["Papaveraceae"] = "7",`
`       ["Schisandraceae"] = "7",`
`       ["Brassicaceae"] = "8",`
`       ["Bretschneideraceae"] = "8",`
`       ["Crassulaceae"] = "8",`
`       ["Droseraceae"] = "8",`
`       ["Moringaceae"] = "8",`
`       ["Nepenthaceae"] = "8",`
`       ["Resedaceae"] = "8",`
`       ["Saxifragaceae"] = "8",`
`       ["Connaraceae"] = "9",`
`       ["Eucommiaceae"] = "9",`
`       ["Hamamelidaceae"] = "9",`
`       ["Pittosporaceae"] = "9",`
`       ["Platanaceae"] = "9",`
`       ["Rosaceae"] = "9",`
`       ["Fabaceae"] = "10",`
`       ["Aceraceae"] = "11",`
`       ["Anacardiaceae"] = "11",`
`       ["Aquifoliaceae"] = "11",`
`       ["Biebersteiniaceae"] = "11",`
`       ["Burseraceae"] = "11",`
`       ["Buxaceae"] = "11",`
`       ["Callitrichaceae"] = "11",`
`       ["Cardiopteridaceae"] = "11",`
`       ["Celastraceae"] = "11",`
`       ["Cneoraceae"] = "11",`
`       ["Coriariaceae"] = "11",`
`       ["Daphniphyllaceae"] = "11",`
`       ["Dichapetalaceae"] = "11",`
`       ["Dipentodontaceae"] = "11",`
`       ["Erythroxylaceae"] = "11",`
`       ["Euphorbiaceae"] = "11",`
`       ["Geraniaceae"] = "11",`
`       ["Icacinaceae"] = "11",`
`       ["Linaceae"] = "11",`
`       ["Malpighiaceae"] = "11",`
`       ["Meliaceae"] = "11",`
`       ["Nitrariaceae"] = "11",`
`       ["Oxalidaceae"] = "11",`
`       ["Pandaceae"] = "11",`
`       ["Peganaceae"] = "11",`
`       ["Plagiopteraceae"] = "11",`
`       ["Polygalaceae"] = "11",`
`       ["Rutaceae"] = "11",`
`       ["Salvadoraceae"] = "11",`
`       ["Simaroubaceae"] = "11",`
`       ["Staphyleaceae"] = "11",`
`       ["Surianaceae"] = "11",`
`       ["Tapisciaceae"] = "11",`
`       ["Tropaeolaceae"] = "11",`
`       ["Zygophyllaceae"] = "11",`
`       ["Actinidiaceae"] = "12",`
`       ["Balsaminaceae"] = "12",`
`       ["Bombacaceae"] = "12",`
`       ["Dilleniaceae"] = "12",`
`       ["Elaeocarpaceae"] = "12",`
`       ["Hippocastanaceae"] = "12",`
`       ["Leeaceae"] = "12",`
`       ["Malvaceae"] = "12",`
`       ["Ochnaceae"] = "12",`
`       ["Pentaphylacaceae"] = "12",`
`       ["Rhamnaceae"] = "12",`
`       ["Sabiaceae"] = "12",`
`       ["Sapindaceae"] = "12",`
`       ["Sladeniaceae"] = "12",`
`       ["Sterculiaceae"] = "12",`
`       ["Theaceae"] = "12",`
`       ["Tiliaceae"] = "12",`
`       ["Vitaceae"] = "12",`
`       ["Alangiaceae"] = "13",`
`       ["Ancistrocladaceae"] = "13",`
`       ["Araliaceae"] = "13",`
`       ["Begoniaceae"] = "13",`
`       ["Bixaceae"] = "13",`
`       ["Cactaceae"] = "13",`
`       ["Caricaceae"] = "13",`
`       ["Cistaceae"] = "13",`
`       ["Clusiaceae"] = "13",`
`       ["Combretaceae"] = "13",`
`       ["Crypteroniaceae"] = "13",`
`       ["Cynomoriaceae"] = "13",`
`       ["Dipterocarpaceae"] = "13",`
`       ["Elaeagnaceae"] = "13",`
`       ["Elatinaceae"] = "13",`
`       ["Flacourtiaceae"] = "13",`
`       ["Frankeniaceae"] = "13",`
`       ["Haloragaceae"] = "13",`
`       ["Hippuridaceae"] = "13",`
`       ["Lecythidaceae"] = "13",`
`       ["Lythraceae"] = "13",`
`       ["Melastomataceae"] = "13",`
`       ["Myrtaceae"] = "13",`
`       ["Nyssaceae"] = "13",`
`       ["Onagraceae"] = "13",`
`       ["Passifloraceae"] = "13",`
`       ["Rhizophoraceae"] = "13",`
`       ["Stachyuraceae"] = "13",`
`       ["Tamaricaceae"] = "13",`
`       ["Tetramelaceae"] = "13",`
`       ["Thymelaeaceae"] = "13",`
`       ["Trapaceae"] = "13",`
`       ["Violaceae"] = "13",`
`       ["Apiaceae"] = "14",`
`       ["Aucubaceae"] = "14",`
`       ["Clethraceae"] = "14",`
`       ["Cornaceae"] = "14",`
`       ["Diapensiaceae"] = "14",`
`       ["Ericaceae"] = "14",`
`       ["Helwingiaceae"] = "14",`
`       ["Mastixiaceae"] = "14",`
`       ["Toricelliaceae"] = "14",`
`       ["Ebenaceae"] = "15",`
`       ["Loganiaceae"] = "15",`
`       ["Myrsinaceae"] = "15",`
`       ["Oleaceae"] = "15",`
`       ["Plumbaginaceae"] = "15",`
`       ["Primulaceae"] = "15",`
`       ["Sapotaceae"] = "15",`
`       ["Styracaceae"] = "15",`
`       ["Symplocaceae"] = "15",`
`       ["Apocynaceae"] = "16",`
`       ["Asclepiadaceae"] = "16",`
`       ["Boraginaceae"] = "16",`
`       ["Convolvulaceae"] = "16",`
`       ["Gentianaceae"] = "16",`
`       ["Hydrophyllaceae"] = "16",`
`       ["Menyanthaceae"] = "16",`
`       ["Polemoniaceae"] = "16",`
`       ["Lamiaceae"] = "17",`
`       ["Solanaceae"] = "17",`
`       ["Verbenaceae"] = "17",`
`       ["Bignoniaceae"] = "18",`
`       ["Gesneriaceae"] = "18",`
`       ["Martyniaceae"] = "18",`
`       ["Orobanchaceae"] = "18",`
`       ["Pedaliaceae"] = "18",`
`       ["Scrophulariaceae"] = "18",`
`       ["Acanthaceae"] = "19",`
`       ["Adoxaceae"] = "19",`
`       ["Annonaceae"] = "19",`
`       ["Berberidaceae"] = "19",`
`       ["Campanulaceae"] = "19",`
`       ["Caprifoliaceae"] = "19",`
`       ["Carlemanniaceae"] = "19",`
`       ["Cucurbitaceae"] = "19",`
`       ["Diervillaceae"] = "19",`
`       ["Dipsacaceae"] = "19",`
`       ["Goodeniaceae"] = "19",`
`       ["Lentibulariaceae"] = "19",`
`       ["Linnaeaceae"] = "19",`
`       ["Morinaceae"] = "19",`
`       ["Myoporaceae"] = "19",`
`       ["Pentaphragmataceae"] = "19",`
`       ["Phrymaceae"] = "19",`
`       ["Plantaginaceae"] = "19",`
`       ["Rubiaceae"] = "19",`
`       ["Sphenocleaceae"] = "19",`
`       ["Stylidiaceae"] = "19",`
`       ["Valerianaceae"] = "19",`
`       ["Asteraceae"] = "20–21",`
`       ["Poaceae"] = "22",`
`       ["Acoraceae"] = "23",`
`       ["Alismataceae"] = "23",`
`       ["Aponogetonaceae"] = "23",`
`       ["Araceae"] = "23",`
`       ["Arecaceae"] = "23",`
`       ["Burmanniaceae"] = "23",`
`       ["Butomaceae"] = "23",`
`       ["Corsiaceae"] = "23",`
`       ["Cymodoceaceae"] = "23",`
`       ["Cyperaceae"] = "23",`
`       ["Hydrocharitaceae"] = "23",`
`       ["Juncaginaceae"] = "23",`
`       ["Lemnaceae"] = "23",`
`       ["Pandanaceae"] = "23",`
`       ["Posidoniaceae"] = "23",`
`       ["Potamogetonaceae"] = "23",`
`       ["Ruppiaceae"] = "23",`
`       ["Scheuchzeriaceae"] = "23",`
`       ["Triuridaceae"] = "23",`
`       ["Typhaceae"] = "23",`
`       ["Zannichelliaceae"] = "23",`
`       ["Zosteraceae"] = "23",`
`       ["Amaryllidaceae"] = "24",`
`       ["Bromeliaceae"] = "24",`
`       ["Cannaceae"] = "24",`
`       ["Centrolepidaceae"] = "24",`
`       ["Commelinaceae"] = "24",`
`       ["Costaceae"] = "24",`
`       ["Dioscoreaceae"] = "24",`
`       ["Eriocaulaceae"] = "24",`
`       ["Flagellariaceae"] = "24",`
`       ["Iridaceae"] = "24",`
`       ["Juncaceae"] = "24",`
`       ["Liliaceae"] = "24",`
`       ["Lowiaceae"] = "24",`
`       ["Marantaceae"] = "24",`
`       ["Musaceae"] = "24",`
`       ["Philydraceae"] = "24",`
`       ["Pontederiaceae"] = "24",`
`       ["Restionaceae"] = "24",`
`       ["Stemonaceae"] = "24",`
`       ["Taccaceae"] = "24",`
`       ["Xyridaceae"] = "24",`
`       ["Zingiberaceae"] = "24",`
`       ["Orchidaceae"] = "25",`
`   },`
`   ["Flora of Chile"] = {`
`       ["Berberidaceae"] = "1",`
`       ["Brassicaceae"] = "1",`
`       ["Capparidaceae"] = "1",`
`       ["Caryophyllaceae"] = "1",`
`       ["Cistaceae"] = "1",`
`       ["Clusiaceae"] = "1",`
`       ["Coriariaceae"] = "1",`
`       ["Droseraceae"] = "1",`
`       ["Elaeocarpaceae"] = "1",`
`       ["Elatinaceae"] = "1",`
`       ["Eucryphiaceae"] = "1",`
`       ["Flacourtiaceae"] = "1",`
`       ["Frankeniaceae"] = "1",`
`       ["Geraniaceae"] = "1",`
`       ["Lactoridaceae"] = "1",`
`       ["Lardizabalaceae"] = "1",`
`       ["Linaceae"] = "1",`
`       ["Magnoliaceae"] = "1",`
`       ["Malpighiaceae"] = "1",`
`       ["Malvaceae"] = "1",`
`       ["Oxalidaceae"] = "1",`
`       ["Papaveraceae"] = "1",`
`       ["Polygalaceae"] = "1",`
`       ["Ranunculaceae"] = "1",`
`       ["Rutaceae"] = "1",`
`       ["Sapindaceae"] = "1",`
`       ["Tropaeolaceae"] = "1",`
`       ["Violaceae"] = "1",`
`       ["Vitaceae"] = "1",`
`       ["Zygophyllaceae"] = "1",`
`       ["Aizoaceae"] = "2",`
`       ["Anacardiaceae"] = "2",`
`       ["Caricaceae"] = "2",`
`       ["Celastraceae"] = "2",`
`       ["Crassulaceae"] = "2",`
`       ["Cucurbitaceae"] = "2",`
`       ["Fabaceae"] = "2",`
`       ["Haloragidaceae"] = "2",`
`       ["Icacinaceae"] = "2",`
`       ["Lythraceae"] = "2",`
`       ["Malesherbiaceae"] = "2",`
`       ["Myrtaceae"] = "2",`
`       ["Onagraceae"] = "2",`
`       ["Passifloraceae"] = "2",`
`       ["Portulacaceae"] = "2",`
`       ["Rhamnaceae"] = "2",`
`       ["Rosaceae"] = "2",`
`       ["Apiaceae"] = "3",`
`       ["Araliaceae"] = "3",`
`       ["Calyceraceae"] = "3",`
`       ["Cornaceae"] = "3",`
`       ["Cunoniaceae"] = "3",`
`       ["Dipsacaceae"] = "3",`
`       ["Loasaceae"] = "3",`
`       ["Rubiaceae"] = "3",`
`       ["Saxifragaceae"] = "3",`
`       ["Valerianaceae"] = "3",`
`       ["Asteraceae"] = "4",`
`       ["Acanthaceae"] = "5",`
`       ["Apocynaceae"] = "5",`
`       ["Asclepiadaceae"] = "5",`
`       ["Bignoniaceae"] = "5",`
`       ["Boraginaceae"] = "5",`
`       ["Campanulaceae"] = "5",`
`       ["Convolvulaceae"] = "5",`
`       ["Epacridaceae"] = "5",`
`       ["Ericaceae"] = "5",`
`       ["Gentianaceae"] = "5",`
`       ["Gesneriaceae"] = "5",`
`       ["Goodeniaceae"] = "5",`
`       ["Hydrophyllaceae"] = "5",`
`       ["Lamiaceae"] = "5",`
`       ["Lentibulariaceae"] = "5",`
`       ["Nolanaceae"] = "5",`
`       ["Oleaceae"] = "5",`
`       ["Orobanchaceae"] = "5",`
`       ["Polemoniaceae"] = "5",`
`       ["Primulaceae"] = "5",`
`       ["Sapotaceae"] = "5",`
`       ["Solanaceae"] = "5",`
`       ["Stylidiaceae"] = "5",`
`       ["Verbenaceae"] = "5",`
`       ["Amaranthaceae"] = "6",`
`       ["Chenopodiaceae"] = "6",`
`       ["Loganiaceae"] = "6",`
`       ["Nyctaginaceae"] = "6",`
`       ["Phytolaccaceae"] = "6",`
`       ["Plantaginaceae"] = "6",`
`       ["Plumbaginaceae"] = "6",`
`       ["Scrophulariaceae"] = "6",`
`   },`

}; volumeTable\["1"\] = volumeTable\["Flora of North America"\] volumeTable\["2"\] = volumeTable\["Flora of China"\] volumeTable\["60"\] = volumeTable\["Flora of Chile"\]

local resources = {

`   ["1"] = "Flora of North America (FNA)",`
`   ["2"] = "Flora of China",`
`   ["3"] = "Chinese Plant Names",`
`   ["4"] = "Moss Flora of China",`
`   ["5"] = "Flora of Pakistan",`
`   ["11"] = "Flora of Missouri",`
`   ["12"] = "Madagascar Catalogue",`
`   ["60"] = "Flora of Chile",`
`   ["101"] = "Flora of Taiwan Checklist",`
`   ["110"] = "Annotated Checklist of the Flowering Plants of Nepal",`
`   ["120"] = "Ornamental Plants from Russia and Adjacent States of the Former Soviet Union",`
`   ["201"] = "Trees and shrubs of the Andes of Ecuador",`
`   ["610"] = "A Checklist for the South China Botanical Garden, Guangzhou, Guangdong Province, P. R. China",`
`   ["1200"] = "Monocot Families (USDA)",`

}

local function getResource(floraID)

`   return resources[floraID]`

end

function p.resource(frame)

`   local floraID = string.match(frame.args[1], "%d+")`
`   if floraID == nil then`
`       return "<span style=\"color: red;\">Please provide a resource number (flora_id). See the list of supported resource numbers at `[`Module:eFloras/doc`](https://zh.wikipedia.org/wiki/Module:eFloras/doc "wikilink")</span>`"`
`   else`
`       local flora = resources[floraID]`
`       if flora == nil then`
`           return "<span style=\"color: red;\">The resource number (flora_id) " .. floraID .. " is not recognized. See the list of supported resource numbers at `[`Module:eFloras/doc`](https://zh.wikipedia.org/wiki/Module:eFloras/doc "wikilink")</span>`"`
`       else`
`           return flora`
`       end`
`   end`

end

function p.volume(frame)

`   local floraID = string.match(frame.args[1], "%d+")`
`   local family = frame.args[2] or frame.args.family`
`   local flora = volumeTable[floraID]`
`   if flora == nil then`
`       return ""`
`   else`
`       local volume = flora[family]`
`       if volume == "error" then`
`           return "19–21 "`
`       elseif volume == nil then`
`           return ""`
`       else`
`           return volume`
`       end`
`   end`

end

function p.name(frame)

`   local name = frame.args[1]`
`   name = string.gsub(name, "^%s*(.*)%s*$", "%1")`
`   name = string.gsub(name, "\'\'\'?", "")`
`   local rank = ""`
`   if name == "" or name == nil then`
`       rank = ""`
`   elseif string.find(name, "aceae") then`
`       rank = "family"`
`   elseif string.find(name, "subsp.") then`
`       rank = "subspecies"`
`   elseif string.find(name, "var.") then`
`       rank = "variety"`
`   elseif string.find(name, "%a%s%a") then`
`       rank = "species"`
`   elseif string.find(name, "%a") then`
`       rank = "genus"`
`   else`
`       error("Module:eFloras could not determine a taxonomic rank for the input that it received: " .. name)`
`   end`
`   if rank == "genus" or rank == "species" then`
`       return "`<i>`" .. name .. "`</i>`"`
`   elseif rank == "species" or rank == "variety" then`
`       local genus, species, lowerRank, lowerRankName = string.match(name, "(%a+)%s+(%a+)%s+(%a+%.)%s+(%a+)") -- Assumes a trinomial name.`
`       if genus == nil or species == nil or lowerRankName == nil or lowerRank == nil then`
`           error("The content being passed to the name function is not recognized")`
`       end`
`       return "`<i>`" .. genus .. " " .. species .. "`</i>` " .. lowerRank .. " `<i>`" .. lowerRankName .. "`</i>`"`
`   elseif rank == "family" then`
`       return name`
`   else`
`       return ""`
`   end`

end

p.get_volume = p.volume

return p

[Category:Pages_using_eFloras_template_with_unsupported_parameter_values](https://zh.wikipedia.org/wiki/Category:Pages_using_eFloras_template_with_unsupported_parameter_values "wikilink") [Category:Pages_using_eFloras_template_with_unsupported_parameter_values](https://zh.wikipedia.org/wiki/Category:Pages_using_eFloras_template_with_unsupported_parameter_values "wikilink")