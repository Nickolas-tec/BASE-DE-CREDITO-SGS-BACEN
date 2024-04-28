# BASE-DE-CREDITO-SGS-BACEN



# ETL DAS SERIES TEMPORAIS DE CREDITO DO BACEN
# TRATAMENTO DE DADOS E CARREGAMENTOS REALIZADO PARA A EQUIPE DE MACRO ECONOMIA DA GEASE (GERENCIA DE ACESSORAMENTO ECONOMICO) DA TESOURARIA GLOBAL DO BANCO DO BRASIL



# O TRATAMENTO CONTA COM A EXTRAÇÃO DOS DADOS, FILTROS E SELEÇÕES DAS VARIAVEIS ADEQUADAS PARA O CONTEXTO DA EQUIPE
# CALCULOS DE VARIAÇÃO MENSAL, TRIMESTRAL E ANUAL
# E POR FIM O CARREGAMENTO DESTES DADOS EM UM ARQUIVO XLSX




# CARREGAMENTO DAS BIBLIOTECAS

library(GetBCBData)
library(tidyverse)
library(dplyr)
library(openxlsx)
library(stringr)
library(tidyverse)
library(tidyr)
library(zoo)

#######################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################
### PLANILHA 1 - DADOS GERAIS
##### NUMERO DAS SERIES TEMPORAIS QUE SERÃO EXTRAIDAS DO SGS-BACEN

# CRIO UM OBJETO QUE RECEBE OS CODIGOS DO BACEN 

dados <- c(dados = 20622, 
           20623, 20624, 
           20625, 20626, 
           20627, 20628,
           20629, 20630, 
           21299, 21300, 
           21301, 21302, 
           22059, 22060, 
           22061, 22062, 
           22063, 22064, 
           22065, 22066, 
           22067, 22068, 
           22069, 22070, 
           20631, 20632, 
           20633, 20634, 
           20635, 20636, 
           20637, 20638,
           20639, 20640, 
           20641, 20642, 
           20643, 20644, 
           20645, 20646, 
           20647, 20648, 
           20649, 20650, 
           20651, 20652, 
           20653, 20654, 
           20655, 20656, 
           20657, 20658, 
           20659, 20660, 
           20661, 20662, 
           20663, 20664, 
           20665, 20666, 
           20667, 20668, 
           20669, 20670, 
           20671, 20672, 
           20673, 20674, 
           20675, 20676, 
           20677, 20678, 
           20679, 20680, 
           20681, 20682, 
           20683, 20684, 
           20685, 20686, 
           20687, 20688, 
           20689, 20690	,
           20691, 20692, 
           20693, 20694, 
           20695, 20696, 
           20697, 20698, 
           20699, 20700, 
           20701, 20702, 
           20703, 20704, 
           20705, 20706, 
           20707, 20708, 
           20709, 20710, 
           20712, 20713,
           20539, 20540, 
           20541, 20542, 
           20543, 20544,
           20545, 20546,
           20547, 20548,
           20549, 20550, 
           20551, 20552, 
           20553, 20554, 
           20555, 20556, 
           20557, 20558,
           20559, 20560, 
           20561, 20562, 
           20563, 20564, 
           20565, 20566, 
           20567, 20568, 
           20569, 20570, 
           20571, 20572, 
           20573, 20574, 
           20575, 20576, 
           20577, 20578, 
           20579, 20580, 
           20581, 20582,
           20583, 20584, 
           20585, 20586, 
           20587, 20588, 
           20589, 20590,
           20591, 20592, 
           20593, 20594,
           20595, 20596,
           20597, 20598,
           20599, 20600, 
           20601, 20602, 
           20603, 20604, 
           20605, 20606, 
           20607, 20608, 
           20609, 20610, 
           20611, 20612,
           20613, 20614, 
           20615, 20616, 
           20617, 20618,
           20620, 20621, 
           13667, 13673, 
           13679, 13685, 
           21082, 21083, 
           21084, 21085, 
           21086, 21087,
           21088, 21089,
           21090, 21091,
           21092, 21093, 
           21094, 21095, 
           21096, 21097,
           21098, 21099,
           21100, 21101, 
           21102, 21103,
           21104, 21105,
           21106, 21107, 
           21108, 21109, 
           21110, 21111,
           21112, 21113, 
           21114, 21115,
           21116, 21117, 
           21118, 21119,
           21120, 21121, 
           21122, 21123,
           21124, 21125, 
           21126, 21127, 
           21128, 21129, 
           21130, 21131, 
           21132, 21133, 
           21134, 21135, 
           21136, 21137, 
           21138, 21139, 
           21140, 21141, 
           21142, 21143, 
           21144, 21145,
           21146, 21147,
           21148, 21149,
           21150, 21151, 
           21152, 21153, 
           21154, 21155, 
           21156, 21157, 
           21159, 21160, 
           29036, 29033,
           29034, 29037, 
           29035, 29038,
           20783, 20784, 
           20785, 20786, 
           20787, 20809, 
           20825, 20826, 
           20837, 21003, 
           21004, 21005,
           21006, 21007, 
           21008, 21009, 
           21010, 21011, 
           21012, 21013, 
           21014, 21015, 
           21016, 21017, 
           21018, 21019, 
           21020, 21021, 
           21022, 21023, 
           21024, 21025,
           21026, 21027, 
           21028, 21029, 
           21030, 21031, 
           21032, 21033, 
           21034, 21035, 
           21036, 21037,
           21038, 21039, 
           21040, 21041, 
           21042, 21043, 
           21044, 21045, 
           21046, 21047, 
           21048, 21049, 
           21050, 21051, 
           21052, 21053, 
           21054, 21055, 
           21056, 21057,
           21058, 21059, 
           21060, 21061, 
           21062, 21063, 
           21064, 21065, 
           21066, 21067,
           21068, 21069, 
           21070, 21071, 
           21072, 21073, 
           21074, 21075, 
           21076, 21077, 
           21078, 21080, 
           21081, 20714,
           20715, 20716,
           20717, 20718,
           20719, 20720, 
           20721, 20722, 
           20723, 20724, 
           20725, 20726, 
           20727, 20728, 
           20729, 20730, 
           20731, 20732, 
           20733, 20734, 
           20735, 20736, 
           20737, 20738, 
           20739, 20740, 
           20741, 20742, 
           20743, 20744, 
           20745, 20746, 
           20747, 20748, 
           20749, 20750, 
           20751, 20752, 
           20753, 20754, 
           20755, 20756, 
           20757, 20758, 
           20759, 20760, 
           20761, 20762, 
           20763, 20764, 
           20765, 20766, 
           20767, 20768, 
           20769, 20770, 
           20771, 20772, 
           20773, 20774, 
           20776, 20777, 
           20778, 20779, 
           20780, 20782, 
           20852, 20853, 
           20854, 20855, 
           20856, 20857,
           20858, 20859, 
           20860, 20861, 
           20862, 20863, 
           20864, 20865, 
           20866, 20867, 
           20868, 20869, 
           20870, 20871, 
           20872, 20873, 
           20874, 20875, 
           20876, 20877, 
           20878, 20879, 
           20880, 20881, 
           20882, 20883, 
           20884, 20885,
           20886, 20887, 
           20888, 20889, 
           20890, 20891, 
           20892, 20893, 
           20894, 20895, 
           20896, 20897, 
           20898, 20899, 
           20900, 20901, 
           20902, 20903, 
           20904, 20905, 
           20906, 20907, 
           20908, 20909, 
           20910, 20911, 
           20912, 20913, 
           20914, 20915, 
           20916, 20917, 
           20918, 20919, 
           20920, 20922, 
           20923, 20924, 
           20925, 20926, 
           20927, 20928, 
           20929, 20930, 
           20931, 20932, 
           20933, 20934, 
           20935, 20936, 
           20937, 20938, 
           20939, 20940, 
           20941, 20942, 
           20943, 20944, 
           20945, 20946, 
           20947, 20948, 
           20949, 20950,
           20951, 20952, 
           20953, 20954, 
           20955, 20956, 
           20957, 20958, 
           20959, 20960, 
           20961, 20962, 
           20963, 20964, 
           20965, 20966, 
           20967, 20968, 
           20969, 20970, 
           20971, 20972, 
           20973, 20974, 
           20975, 20976, 
           20977, 20978, 
           20979, 20980, 
           20981, 20982, 
           20983, 20984, 
           20985, 20986, 
           20987, 20988, 
           20989, 20990, 
           20991, 20992, 
           20993, 20994, 
           20995, 20996,
           20997, 20998, 
           20999, 21001, 
           21002, 2007, 
           2043,  12106, 
           12150, 21277, 
           21278, 21279, 
           21359, 21360, 
           21362, 22019, 
           22020, 22021, 
           22022, 22023, 
           22024, 22025, 
           22026, 22027, 
           22028, 22029, 
           22030, 22034, 
           22036, 22037, 
           22039, 22041, 
           22042, 22043, 
           22044, 22047, 
           22050, 22051, 
           22052) 

################################################################################


first_date = '1980-01-01' # DEFINO UMA DATA DE INICIO
last_date <- Sys.Date() # DEFINO A DATA DO FIM DA CAPTURA DOS DADOS


#### EXTRAINDO AS SERIES DO BACEN, DE ACORDO COM CADA CODIGO QUE FOI ARMAZENADO EM DADOS 

# UTILIZO A FUNÇÃO GBCD_GET_SERIES DO PACOTE "GETBCBDATA" PARA EXTRAIR AS SERIES TEMPORAIS
# DEFINO ID = DADOS, DEFINE O ID DAS SERIES QUE DESEJO IMPORTAR
# FIRST.DATE = FIRST_DATE, DEFINE A PRIMERIA DATA DA SERIE
# LAST.DATE = LAST_DATE, DEGINE A ULTIMA DATA DA SERIE
# USE.MEMOISE = FALSE, DESATIVA O SISTEMA DE CACHE

dados <- gbcbd_get_series(id = dados,
                          first.date = first_date,
                          last.date = last_date,
                          use.memoise = FALSE)


### RENOMEANDO AS COLUNAS DO DATAFRAME
colnames(dados) = c('Data', 'Valor', 'Serie','xx') 

### EXCLUINDO A COLUNA XX

# E CRIADO O VETOR EXCLUIR, QUE TEM A STRING "XX"
excluir <- c("xx")
# AQUI ATUALIZAMOS O DATAFRAME PARA EXCLUIR AS COLUNAS CUJOS OS NOMES ESTÃO NO VETOR
# NAMES(DADOS): RETORNA OS NOMES DAS COLUNAS DO DATAFRAME
# %IN% EXCLUIR: VERIFICA QUAIS NOMES DE COLUNAS ESTÃO NO VETOR
# !(...): O OPERADOR DE NEGAÇÃO INVERTE A CONDIÇÃO
# DADOS[, ...]: SELECIONA TODAS AS LINHAS E AS COLUNAS QUE CORRESPONDEM A CONDIÇÃO 
dados <- dados[,!(names(dados)%in% excluir)]


# DISTRIBUINDO OS DADOS EM COLUNAS 
# A FUNÇÃO PIVOT_WIDER E UTILIZADA PARA TRANSFORMAR DADOS LONGOS EM UM FORMATO WIDE
# A FUNÇÃO ARRANGE E UTILIZADA PARA ORDENAR AS LINHAS PELA COLUNA DATA, PARA QUE OS DADOS ESTEJAM EM ORDEM CRONOLOGICA

dados <- dados %>% 
  pivot_wider(names_from = Serie, values_from = Valor) %>%
  arrange(Data) 


# AQUI ATUALIZO O DATAFRAME SELECIONANDO AS VARIAVEIS MAIS IMPORTANTES PARA MIM NO MOMENTO

dados <- dados %>%
  select("Data",
         "20539", "20540",
         "20541", "20542",
         "20543", "20570",
         "20593", "20594",
         "20606", "21082",
         "21083", "21084",
         "21085", "21086",
         "21112", "21132",
         "21133")
  
# A COLUNA 20539 RETORNOU EM ALGUMAS LINHAS O "0"
# ENTÃO IREMOS SUBSTITUIR TODOS OS VALORES 0 POR NA, QUE REPRESENTA VALORES AUSENTES

dados$`20539`[dados$`20539` == "0"] <- NA



########################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################
### PLANILHA 2 - VOLUME E VARIAÇÕES MENSAIS, TRIMESTRAL E ANUAL
##### NUMERO DAS SERIES TEMPORAIS QUE SERÃO EXTRAIDAS DO SGS-BACEN

# CRIANDO O VETOR QUE POSSUI AS SERIES DO BACEN ESTATISTICAS DE CREDITO

credito <- c(credito = 20539, 20540,
             20541, 20542,
             20543, 20570,
             20593, 20594,
             20606, 21082,
             21083, 21084,
             21085, 21086,
             21112, 21132,
             21133, 21145 )



first_date = '1980-01-01' # DEFINO UMA DATA DE INICIO
last_date <- Sys.Date() # DEFINO A DATA DO FIM DA CAPTURA DOS DADOS



#### EXTRAINDO AS SERIES DO BACEN, DE ACORDO COM CADA CODIGO QUE FOI ARMAZENADO EM CREDITO 

# UTILIZO A FUNÇÃO GBCD_GET_SERIES DO PACOTE "GETBCBDATA" PARA EXTRAIR AS SERIES TEMPORAIS
# DEFINO ID = CREDITO, DEFINE O ID DAS SERIES QUE DESEJO IMPORTAR
# FIRST.DATE = FIRST_DATE, DEFINE A PRIMERIA DATA DA SERIE
# LAST.DATE = LAST_DATE, DEGINE A ULTIMA DATA DA SERIE
# USE.MEMOISE = FALSE, DESATIVA O SISTEMA DE CACHE

volume <- gbcbd_get_series(id = credito,
                           first.date = first_date,
                           last.date = last_date,
                           use.memoise = FALSE)



### RENOMEANDO AS COLUNAS DO DATAFRAME
colnames(volume) = c('Data', 'Valor', 'Serie','xx') 


# E CRIADO O VETOR EXCLUIR, QUE TEM A STRING "XX"
excluir <- c("xx")
# AQUI ATUALIZAMOS O DATAFRAME PARA EXCLUIR AS COLUNAS CUJOS OS NOMES ESTÃO NO VETOR
# NAMES(VOLUME): RETORNA OS NOMES DAS COLUNAS DO DATAFRAME
# %IN% EXCLUIR: VERIFICA QUAIS NOMES DE COLUNAS ESTÃO NO VETOR
# !(...): O OPERADOR DE NEGAÇÃO INVERTE A CONDIÇÃO
# VOLUME[, ...]: SELECIONA TODAS AS LINHAS E AS COLUNAS QUE CORRESPONDEM A CONDIÇÃO
volume <- volume[,!(names(volume)%in% excluir)]


# DISTRIBUINDO OS DADOS EM COLUNAS 
# A FUNÇÃO PIVOT_WIDER E UTILIZADA PARA TRANSFORMAR DADOS LONGOS EM UM FORMATO WIDE
# A FUNÇÃO ARRANGE E UTILIZADA PARA ORDENAR AS LINHAS PELA COLUNA DATA, PARA QUE OS DADOS ESTEJAM EM ORDEM CRONOLOGICA
volume <- volume %>% 
  pivot_wider(names_from = Serie, values_from = Valor)%>%
  arrange(Data)


# AQUI RENOMEIO AS COLUNAS DO DATAFRAME VOLUME 
colnames(volume) <- c("Data",
                      "Saldo da carteira de crédito - Total - 20539",
                      "Saldo da carteira de crédito - Pessoas jurídicas - Total - 20540",
                      "Saldo da carteira de crédito - Pessoas físicas - Total - 20541",
                      "Saldo da carteira de crédito com recursos livres - Total - 20542",
                      "Saldo da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 20543",
                      "Saldo da carteira de crédito com recursos livres - Pessoas físicas - Total - 20570",
                      "Saldo da carteira de crédito com recursos direcionados - Total - 20593",
                      "Saldo da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 20594",
                      "Saldo da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 20606",
                      "Inadimplência da carteira de crédito - Total - 21082",
                      "Inadimplência da carteira de crédito - Pessoas jurídicas - Total - 21083",
                      "Inadimplência da carteira de crédito - Pessoas físicas - Total - 21084",
                      "Inadimplência da carteira de crédito com recursos livres - Total - 21085",
                      "Inadimplência da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 21086",
                      "Inadimplência da carteira de crédito com recursos livres - Pessoas físicas - Total - 21112",
                      "Inadimplência da carteira de crédito com recursos direcionados - Total - 21132",
                      "Inadimplência da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 21133",
                      "Inadimplência da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 21145")



# A COLUNA "Saldo da carteira de crédito - Total - 20539" RETORNOU EM ALGUMAS LINHAS O "0"
# ENTÃO IREMOS SUBSTITUIR TODOS OS VALORES 0 POR NA, QUE REPRESENTA VALORES AUSENTES
volume$`Saldo da carteira de crédito - Total - 20539`[volume$`Saldo da carteira de crédito - Total - 20539`== "0"] <- NA





# UTILIZO O SELECT PARA SELECIONAR SOMENTE AS VARIAVEIS DE SALDOS
saldos <- volume %>%
  select("Data",
         "Saldo da carteira de crédito - Total - 20539",
         "Saldo da carteira de crédito - Pessoas jurídicas - Total - 20540",
         "Saldo da carteira de crédito - Pessoas físicas - Total - 20541",
         "Saldo da carteira de crédito com recursos livres - Total - 20542",
         "Saldo da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 20543",
         "Saldo da carteira de crédito com recursos livres - Pessoas físicas - Total - 20570",
         "Saldo da carteira de crédito com recursos direcionados - Total - 20593",
         "Saldo da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 20594",
         "Saldo da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 20606")




# UTILIZO O SELECT PARA SELECIONAR AS VARIAVEIS DE INADIPLENCIA E CRIAR UM DATAFRAME SOMENTE COM ESSAS VARIAVEIS
inadiplencia <- volume %>%
  select("Data",
         "Inadimplência da carteira de crédito - Total - 21082",
         "Inadimplência da carteira de crédito - Pessoas jurídicas - Total - 21083",
         "Inadimplência da carteira de crédito - Pessoas físicas - Total - 21084",
         "Inadimplência da carteira de crédito com recursos livres - Total - 21085",
         "Inadimplência da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 21086",
         "Inadimplência da carteira de crédito com recursos livres - Pessoas físicas - Total - 21112",
         "Inadimplência da carteira de crédito com recursos direcionados - Total - 21132",
         "Inadimplência da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 21133",
         "Inadimplência da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 21145")



#####################################################################################

# CALCULO DE VARIAÇÃO MENSAL COM VARIAVEIS DE CREDITO, PLANILHA VOLUME / CREDITO

# E CRIADO UM NOVO DATAFRAMNE A PARTIR DO VOLUME
# A FUNÇÃO MUTATE VAI CRIAR A COLUNA VAR MENSAL SALDO CARTEIRA DE CREDITO TOTAL 20539
# DEPOIS E CALCULADO A RAZAÃO ENTRE O VALOR ATUAL DA COLUNA 20539 E O SEU VALOR ANTERIOR (LAG DE 1)
# ((...) - 1) * 100: SUBTRAI 1 DO RESULTADO DA RAZÃO CALCULADA E MULTIPLICA POR 100, OBTENDO O VALOR DA VARIAÇÃO MENSAL

variacao_mensal <- volume %>%
  
  mutate(Variacao_mensal_Saldo_da_carteira_de_crédito_Total_20539 = ((`Saldo da carteira de crédito - Total - 20539` / 
                              lag( `Saldo da carteira de crédito - Total - 20539`,
                                               1)) - 1) * 100)


# AQUI O DATAFRAME VARIACAO_MENSAL E ATUALIZADO
# SENDO REALIZADO O MESMO CALCULO DE PERCENTUAL MENSAL E ADICIONANDO UMA NOVA COLUNA 
# QUE NESSE CASO CONTEM A VARIACAO DA SERIE TEMPORAL 20540
# E ASSIM SERÁ COM TODAS AS VARIAVEIS DE VOLUME

variacao_mensal <- variacao_mensal %>%
  mutate(variacao_mensal_Saldo_da_carteira_de_crédito_Pessoas_jurídicas_Total_20540 = ((`Saldo da carteira de crédito - Pessoas jurídicas - Total - 20540` / 
                              lag(`Saldo da carteira de crédito - Pessoas jurídicas - Total - 20540`,
                                              1)) -1) * 100)






variacao_mensal <- variacao_mensal %>%
  mutate(variacao_mensal_Saldo_da_carteira_de_crédito_Pessoas_físicas_Total_20541 = ((`Saldo da carteira de crédito - Pessoas físicas - Total - 20541` / 
                              lag(`Saldo da carteira de crédito - Pessoas físicas - Total - 20541`,
                                  1)) -1) * 100)




variacao_mensal <- variacao_mensal %>%
  mutate(variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_livres_Total_20542 = ((`Saldo da carteira de crédito com recursos livres - Total - 20542` / 
                              lag(`Saldo da carteira de crédito com recursos livres - Total - 20542`,
                                  1)) -1) * 100)



variacao_mensal <- variacao_mensal %>%
  mutate(variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_jurídicas_Total_20543 = ((`Saldo da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 20543` / 
                              lag(`Saldo da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 20543`,
                                  1)) -1) * 100)




variacao_mensal <- variacao_mensal %>%
  mutate(variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_físicas_Total_20570 = ((`Saldo da carteira de crédito com recursos livres - Pessoas físicas - Total - 20570` / 
                              lag(`Saldo da carteira de crédito com recursos livres - Pessoas físicas - Total - 20570`,
                                  1)) -1) * 100)




variacao_mensal <- variacao_mensal %>%
  mutate(variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Total_20593 = ((`Saldo da carteira de crédito com recursos direcionados - Total - 20593` / 
                              lag(`Saldo da carteira de crédito com recursos direcionados - Total - 20593`,
                                  1)) -1) * 100)




variacao_mensal <- variacao_mensal %>%
  mutate(variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_jurídicas_Total_20594 = ((`Saldo da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 20594` / 
                              lag(`Saldo da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 20594`,
                                  1)) -1) * 100)







variacao_mensal <- variacao_mensal %>%
  mutate(variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_físicas_Total_20606= ((`Saldo da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 20606` / 
                              lag(`Saldo da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 20606`,
                                  1)) -1) * 100)





# AGORA AQUI REALIZAMOS UMA ATUALIZAÇÃO DO DATAFRAME VARIACAO_MENSAL
# PORÉM COM UM SELECT, SELECIONANDO SOMENTE AS COLUNAS QUE CONTÉM AS VARIAÇÕES DAS VARIAVEIS

variacao_mensal <- variacao_mensal %>%
  
  select(Data,
         Variacao_mensal_Saldo_da_carteira_de_crédito_Total_20539,
         variacao_mensal_Saldo_da_carteira_de_crédito_Pessoas_jurídicas_Total_20540,
         variacao_mensal_Saldo_da_carteira_de_crédito_Pessoas_físicas_Total_20541,
         variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_livres_Total_20542,
         variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_jurídicas_Total_20543,
         variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_físicas_Total_20570,
         variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Total_20593,
         variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_jurídicas_Total_20594,
         variacao_mensal_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_físicas_Total_20606)


  
  
###########################################################################################################################################################

# CALCULO VARIAÇÃO TRIMESTRAL

# PARA CALCULAR A VARIAÇÃO PERCENTUAL TRIMESTRAL DO SALDO DA CARTEIRA DE CREDITO TOTAL
# E CRIADO O DATAFRAME VARIACAO_TRIMESTRAL A PARTIR DO DATAFRAME VOLUME
# AQUI SIGO O MESMO PRINCIPIO DA VARIACAO MENSAL, CRIO UMA NOVA COLUNA CHAMADA VARIACAO TRIMESTRAL E A SERIE TEMPORAL
# E CALCULO A RAZÃO ENTRE O VALOR ATUAL DA COLUNA 20539 E O VALOR DA MESMA TRÊS PERIODOS ATRAS (TRIMESTRALMENTE)
# UTILIZANDO O LAG
# DEPOIS SUBTRAI-SE POR 1 DO RESULTADO DA RAZÃO E MULTIPLICA-SE POR 100 CONVERTENDO A VARIAÇÃO EM UMA PORCENTAGEM

variacao_trimestral <- volume %>%
  
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_Total_20539 = ((`Saldo da carteira de crédito - Total - 20539` / 
                                         lag( `Saldo da carteira de crédito - Total - 20539`,
                                               3)) - 1) * 100)




# AQUI O DATAFRAME VARIACAO_TRIMESTRAL E ATUALIZADO
# SENDO REALIZADO O MESMO CALCULO DE PERCENTUAL TRIMESTRAL E ADICIONANDO UMA NOVA COLUNA 
# QUE NESSE CASO CONTEM A VARIACAO DA SERIE TEMPORAL 20540
# E ASSIM SERÁ COM TODAS AS VARIAVEIS DE VOLUME

variacao_trimestral <- variacao_trimestral %>%
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_Pessoas_jurídicas_Total_20540 = ((`Saldo da carteira de crédito - Pessoas jurídicas - Total - 20540` / 
                                         lag(`Saldo da carteira de crédito - Pessoas jurídicas - Total - 20540`,
                                              3)) -1) * 100)




variacao_trimestral <- variacao_trimestral %>%
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_Pessoas_físicas_Total_20541 = ((`Saldo da carteira de crédito - Pessoas físicas - Total - 20541` / 
                                         lag(`Saldo da carteira de crédito - Pessoas físicas - Total - 20541`,
                                             3)) -1) * 100)






variacao_trimestral <- variacao_trimestral %>%
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_livres_Total_20542 = ((`Saldo da carteira de crédito com recursos livres - Total - 20542` / 
                                         lag(`Saldo da carteira de crédito com recursos livres - Total - 20542`,
                                             3)) -1) * 100)







variacao_trimestral <- variacao_trimestral %>%
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_jurídicas_Total_20543 = ((`Saldo da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 20543` / 
                                         lag(`Saldo da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 20543`,
                                             3)) -1) * 100)








variacao_trimestral <- variacao_trimestral %>%
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_físicas_Total_20570 = ((`Saldo da carteira de crédito com recursos livres - Pessoas físicas - Total - 20570` / 
                                         lag(`Saldo da carteira de crédito com recursos livres - Pessoas físicas - Total - 20570`,
                                             3)) -1) * 100)








variacao_trimestral <- variacao_trimestral %>%
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Total_20593 = ((`Saldo da carteira de crédito com recursos direcionados - Total - 20593` / 
                                         lag(`Saldo da carteira de crédito com recursos direcionados - Total - 20593`,
                                             3)) -1) * 100)










variacao_trimestral <- variacao_trimestral %>%
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_jurídicas_Total_20594 = ((`Saldo da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 20594` / 
                                         lag(`Saldo da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 20594`,
                                             3)) -1) * 100)










variacao_trimestral <- variacao_trimestral %>%
  mutate(Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_físicas_Total_20606 = ((`Saldo da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 20606` / 
                                         lag(`Saldo da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 20606`,
                                             3)) -1) * 100)



# AQUI REALIZO A ATUALIZAÇAO DO DATAFRAME ATRAVES DO SELECT, SELECIONANDO SOMENTE AS COLUNAS COM A VARIAÇÃO TRIMESTRAL

variacao_trimestral <- variacao_trimestral %>%
  select(Data,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_Total_20539,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_Pessoas_jurídicas_Total_20540,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_Pessoas_físicas_Total_20541,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_livres_Total_20542,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_jurídicas_Total_20543,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_físicas_Total_20570,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Total_20593,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_jurídicas_Total_20594,
         Variacao_trimestral_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_físicas_Total_20606)

##########################################################################################################


# CALCULO VARIACAO 12 MESES

# AGORA CALCULAMOS A VARIAÇÃO PERCENTUAL ANUAL DO SALDO DA CARTEIRA DE CREDITO
# SEMPRE CRIANDO UM NOVO DATAFRAME A PARTIR DO VOLUME
# O MUTATE REALIZANDO A CRIAÇÃO DA NOVA COLUMA VARIACAO 12 MESES
# CALCULAMOS A RAZÃO ENTRE O VALOR ANUAL DA COLUNA E O VALOR DA MESMA DOZE PERIODOS ATRAS (ANUALMENTE)
# UTILIZANDO O LAG, E DEPOIS SUBTRAI-SE 1 DO RESULTADO DA RAZÃO E MULTIPLICA POR 100 PARA CONVERTER A VARIAÇÃO EM UMA PORCENTAGEM


variacao_12_meses <- volume %>%
  
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_Total_20539 = ((`Saldo da carteira de crédito - Total - 20539` / 
                                       lag( `Saldo da carteira de crédito - Total - 20539`,
                                               12)) - 1) * 100)






# AQUI O DATAFRAME VARIACAO_12_MESES E ATUALIZADO
# SENDO REALIZADO O MESMO CALCULO DE PERCENTUAL ANUAL E ADICIONANDO UMA NOVA COLUNA 
# QUE NESSE CASO CONTEM A VARIACAO DA SERIE TEMPORAL 20540
# E ASSIM SERÁ COM TODAS AS VARIAVEIS DE VOLUME

variacao_12_meses <- variacao_12_meses %>%
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_Pessoas_jurídicas_Total_20540 = ((`Saldo da carteira de crédito - Pessoas jurídicas - Total - 20540` / 
                              lag(`Saldo da carteira de crédito - Pessoas jurídicas - Total - 20540`,
                                              12)) -1) * 100)




variacao_12_meses <- variacao_12_meses %>%
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_Pessoas_físicas_Total_20541 = ((`Saldo da carteira de crédito - Pessoas físicas - Total - 20541` / 
                                       lag(`Saldo da carteira de crédito - Pessoas físicas - Total - 20541`,
                                           12)) -1) * 100)






variacao_12_meses <- variacao_12_meses %>%
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_livres_Total_20542 = ((`Saldo da carteira de crédito com recursos livres - Total - 20542` / 
                                       lag(`Saldo da carteira de crédito com recursos livres - Total - 20542`,
                                           12)) -1) * 100)







variacao_12_meses <- variacao_12_meses %>%
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_jurídicas_Total_20543 = ((`Saldo da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 20543` / 
                                       lag(`Saldo da carteira de crédito com recursos livres - Pessoas jurídicas - Total - 20543`,
                                           12)) -1) * 100)






variacao_12_meses <- variacao_12_meses %>%
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_físicas_Total_20570 = ((`Saldo da carteira de crédito com recursos livres - Pessoas físicas - Total - 20570` / 
                                       lag(`Saldo da carteira de crédito com recursos livres - Pessoas físicas - Total - 20570`,
                                           12)) -1) * 100)







variacao_12_meses <- variacao_12_meses %>%
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Total_20593 = ((`Saldo da carteira de crédito com recursos direcionados - Total - 20593` / 
                                       lag(`Saldo da carteira de crédito com recursos direcionados - Total - 20593`,
                                           12)) -1) * 100)











variacao_12_meses <- variacao_12_meses %>%
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_jurídicas_Total_20594 = ((`Saldo da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 20594` / 
                                       lag(`Saldo da carteira de crédito com recursos direcionados - Pessoas jurídicas - Total - 20594`,
                                           12)) -1) * 100)












variacao_12_meses <- variacao_12_meses %>%
  mutate(variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_físicas_Total_20606 = ((`Saldo da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 20606` / 
                                       lag(`Saldo da carteira de crédito com recursos direcionados - Pessoas físicas - Total - 20606`,
                                           12)) -1) * 100)




# AQUI REALIZO A ATUALIZAÇAO DO DATAFRAME ATRAVES DO SELECT, SELECIONANDO SOMENTE AS COLUNAS COM A VARIAÇÃO EM 12 MESES

variacao_12_meses <- variacao_12_meses %>%
  
  select(Data,
         variacao_12_meses_Saldo_da_carteira_de_crédito_Total_20539,
         variacao_12_meses_Saldo_da_carteira_de_crédito_Pessoas_jurídicas_Total_20540,
         variacao_12_meses_Saldo_da_carteira_de_crédito_Pessoas_físicas_Total_20541,
         variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_livres_Total_20542,
         variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_jurídicas_Total_20543,
         variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_livres_Pessoas_físicas_Total_20570,
         variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Total_20593,
         variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_jurídicas_Total_20594,
         variacao_12_meses_Saldo_da_carteira_de_crédito_com_recursos_direcionados_Pessoas_físicas_Total_20606
  )


#################################################################################################################################################


### PLANILHA 3 - SALDOS DEFLACIONADOS
##### NUMERO DAS SERIES TEMPORAIS QUE SERÃO EXTRAIDAS DO SGS-BACEN

# CRIO UM OBJETO QUE RECEBE OS CODIGOS DO BACEN 

credito_saldo <- c(credito = 433,
                     20539, 20540,  20541)



first_date = '1980-01-01'  # DEFINO UMA DATA DE INICIO
last_date <- Sys.Date() # DEFINO A DATA DO FIM DA CAPTURA DOS DADOS




#### EXTRAINDO AS SERIES DO BACEN, DE ACORDO COM CADA CODIGO QUE FOI ARMAZENADO EM CREDITO_SALDO

# UTILIZO A FUNÇÃO GBCD_GET_SERIES DO PACOTE "GETBCBDATA" PARA EXTRAIR AS SERIES TEMPORAIS
# DEFINO ID = CREDITO_SALDO, DEFINE O ID DAS SERIES QUE DESEJO IMPORTAR
# FIRST.DATE = FIRST_DATE, DEFINE A PRIMERIA DATA DA SERIE
# LAST.DATE = LAST_DATE, DEGINE A ULTIMA DATA DA SERIE
# USE.MEMOISE = FALSE, DESATIVA O SISTEMA DE CACHE

saldo <- gbcbd_get_series(id = credito_saldo,
                          first.date = first_date,
                          last.date = last_date,
                          use.memoise = FALSE)


# RENOMEANDO AS COLUNAS DE SALDO

colnames(saldo) = c('date', 'Valor', 'Serie','xx') 



# E CRIADO O VETOR EXCLUIR, QUE TEM A STRING "XX"
excluir <- c("xx")
# AQUI ATUALIZAMOS O DATAFRAME PARA EXCLUIR AS COLUNAS CUJOS OS NOMES ESTÃO NO VETOR
# NAMES(VOLUME): RETORNA OS NOMES DAS COLUNAS DO DATAFRAME
# %IN% EXCLUIR: VERIFICA QUAIS NOMES DE COLUNAS ESTÃO NO VETOR
# !(...): O OPERADOR DE NEGAÇÃO INVERTE A CONDIÇÃO
# VOLUME[, ...]: SELECIONA TODAS AS LINHAS E AS COLUNAS QUE CORRESPONDEM A CONDIÇÃO
saldo <- saldo[,!(names(saldo)%in% excluir)]




# DISTRIBUINDO OS DADOS EM COLUNAS 
# A FUNÇÃO PIVOT_WIDER E UTILIZADA PARA TRANSFORMAR DADOS LONGOS EM UM FORMATO WIDE
# A FUNÇÃO ARRANGE E UTILIZADA PARA ORDENAR AS LINHAS PELA COLUNA DATA, PARA QUE OS DADOS ESTEJAM EM ORDEM CRONOLOGICA

saldo <- saldo %>% 
  pivot_wider(names_from = Serie, values_from = Valor)


# RENOMEANDO AS COLUNAS DO DATAFRAME SALDO
colnames(saldo) = c('data', 'ipca', 'saldo_total', 'saldo_pj', 'saldo_pf')


# A COLUNA SALDO_TOTAL RETORNOU EM ALGUMAS LINHAS O "0"
# ENTÃO IREMOS SUBSTITUIR TODOS OS VALORES 0 POR NA, QUE REPRESENTA VALORES AUSENTES

saldo$saldo_total[saldo$saldo_total == '0'] <- NA


#########################################################################################################################################################################################################################
#########################################################################################################################################################################################################################

# A FUNÇÃO MULT_DESCOLADO ESTA AJUSTANDO UMA SERIE DE VALORES ATRAVES DO IPCA
# PARA CADA PONTO NO TEMPO, COMEÇANDO PELO ULTIMO VALOR E INDO ATE O PRIMEIRO
# O ULTIMO VALOR DA SERIE E DEFINIDO COMO 1, E OS VALORES ANTERIORES AJUSTADOS DE FORMA ACUMULATIVA PELO IPCA
# O RESULTADO E UM DATAFRAME COM AS DATAS E MULTIPLICADORES AJUSTADOS

mult_descolado <- function(v,ipca,data){
  ultimo_dado = last(v[!is.na(v)]) # SELECIONA O ULTIMO VALOR NÃO - NA DO VETOR V
  n = which(v==ultimo_dado) # ENCONTRA A POSIÇÃO DESTE ULTIMO VALOR NO VETOR
  data = data[1:n] # REDUZ O VETOR DE DATAS ATÉ A POSIÇÃO DO ULTIMO DADO
  v = v[1:n] # REDUZ O VETOR V ATE A POSIÇÃO DO ULTIMO DADO
  v[n] = 1 # DEFINE O ULTIMO VALOR DO VETOR V COMO 1
  i = n - 1 # INICIA UM INDICE I COMO SENDO A POSIÇÃO ANTERIOR AO ULTIMO VALOR DE V
  while(i >= 1){ # ENQUANTO I FOR MAIOR OU IGUAL A 1, E EXECUTADO O LOOP
    v[i] <- v[i+1]*(1+ipca[i+1]/100) # ATUALIZA V[I] COM O O VALOR AJUSTADO PELO IPCA
    i = i - 1  # DECREMENTA O INDICE I
  }
  df = data.frame(data,mult = v) # CRIA UM DATAFRAME COM AS DATAS E OS MULTIPLICADORES CALCULADOS
  return(df) # RETORNA O DATAFRAME CRIADO
}

# CHAMAMOS A FUNÇÃO E PASSAMOS TRES ARGUMENTOS
# SALDOS$SALDO_TOTAL, SALDOS$IPCA E SALDOS$DATA
# A FUNÇÃO CALCULA O MULTIPLICADOR AJUSTADO, COM BASE NOS VALORES TOTAIS DE SALDO, NO IPCA E NAS DATAS
# O RESULTADO E ARMAZENADO NO OBJETO MULT
mult <- mult_descolado(saldo$saldo_total,saldo$ipca,saldo$data)
saldo <- left_join(saldo,mult) # AQUI REALIZO O LEFT JOIN DO DATAFRAME SALDO COM O OBJETO MULT
# A PARTIR DISSO TODOS OS REGISTROS DO DATAFRAME SALDO VÃO SER MANTIDOS, E AS COLUNAS DO OBJETO MULT VÃO SER ADICIONADAS NO SALDO



# CRIO A VARIAVEL CREDITO_DEFLACIONADO ATRIBUINDO OS DAODS DE SALDO
credito_deflacionado <- saldo 


# AQUI CALCULO O SALDO TOTAL REAL MULTIPLICANDO UM MULTIPLICAODR DE DEFLAÇÃO 
#(CREDITO_DEFLACIONADO$MULT) PELO SALDO TOTAL NOMINAL (CREDITO_DEFLACIONADO$SALDO_TOTAL)
# E O RESULTADO E ARMAZENADO NA NOVA COLUNA SALDO_TOTAL_REAL
credito_deflacionado$saldo_total_real <- credito_deflacionado$mult*credito_deflacionado$saldo_total

# SIMILAR A LINHA DE CIMA, O CODIGO CALCULA O SALDO REAL PARA PESSOAS JURIDICAS, MULTIPLICANDO O MESMO MULTIPLICADOR DE DEFLAÇÃO
# PELO SALDO NOMINAL DE PESSOAS JURIDICAS. O RESULTADO E ATRIBUIDO A SALDO_PJ_REAL
credito_deflacionado$saldo_pj_real <- credito_deflacionado$mult*credito_deflacionado$saldo_pj


# ESTE TRECHO FAZ O MESMO CALCULO PARA PESSOAS FISICAS
credito_deflacionado$saldo_pf_real <- credito_deflacionado$mult*credito_deflacionado$saldo_pf



# AQUI ATUALIZO O CREDITO DEFLACIONADO SELECIONANDO AS VARIAVEIS MAIS IMPORTANTES PARA O MEU CONTEXTO
credito_deflacionado <- credito_deflacionado %>% 
  select(data, ipca, saldo_total, saldo_pj, saldo_pf, saldo_total_real, saldo_pj_real, saldo_pf_real)




################################################################################################################################################################################################################
#######################################################################################################################################################################################################################

# CALCULO DE VARIAÇÃO MENSAL SALDOS DEFLACIONADOS

# CRIO A VARIAVEL VAR MENSAL SALDOS DEFLACIONADOS A PARTIR DOS DADOS DE CREDITO DEFLACIONADO
# O MUTATE CRIA A COLUNA VARIACAL MENSAL SALDO TOTAL REAL
# O VALOR ATUAL DE SALDO TOTAL REAL E DIVIDO PELO VALOR ANTERIOR (LAG) DE SALDO TOTAL REAL
# A FUNÇÃO LAG DESLOCA OS DADOS POR UM PERIODO ESPECIFICADO, NO CASO O 1, INDICANDO O VALOR DO MES ANTERIOR
# O RESULTADO E SUBTRAIDO POR 1 PARA ENCONTRAR A VARIAÇÃO PROPORCIONAL E DEPOIS E MULTIPLICADA POR 100 CONVERTENDO EM PORCENTAGEM

var_mensal_saldos_deflacionados <- credito_deflacionado %>%
  
  mutate(variacao_mensal_saldo_total_real = ((`saldo_total_real` / 
                              lag( `saldo_total_real`,
                                   1)) - 1) * 100)



# AQUI O DATAFRAME VARIACAO_MENSAL SALDOS DEFLACIONADOS E ATUALIZADO
# SENDO REALIZADO O MESMO CALCULO DE PERCENTUAL MENSAL E ADICIONANDO UMA NOVA COLUNA 
# E ASSIM SERÁ COM TODAS AS VARIAVEIS DE CREDITO DEFLACIONADO

var_mensal_saldos_deflacionados <- var_mensal_saldos_deflacionados %>%
  
  mutate(variacao_mensal_saldo_pessoas_juridicas_real = ((`saldo_pj_real` / 
                                                lag( `saldo_pj_real`,
                                                     1)) - 1) * 100)



var_mensal_saldos_deflacionados <-  var_mensal_saldos_deflacionados %>%
  
  mutate(variacao_mensal_saldo_pessoas_fisicas_real = ((`saldo_pf_real` / 
                                             lag( `saldo_pf_real`,
                                                  1)) - 1) * 100)



# AQUI ATUALIZO O DATAFRAME E SELECIONO SOMENTE AS COLUNAS DATA, E AS VARIAÇÕES MENSAIS

var_mensal_saldos_deflacionados <- var_mensal_saldos_deflacionados %>%
  select("data","variacao_mensal_saldo_total_real",
         "variacao_mensal_saldo_pessoas_juridicas_real",
         "variacao_mensal_saldo_pessoas_fisicas_real")






################################################################################################################################################################################################
#######################################################################################################################################################################################################

# VARIAÇÃO TRIMESTRAL SALDO DEFLACIONADO
# PARA CALCULAR A VARIAÇÃO PERCENTUAL TRIMESTRAL DO SALDOS DEFLACIONADOS
# E CRIADO O DATAFRAME VARIACAO_TRIMESTRAL SALDOS DEFLACIONADOS A PARTIR DO DATAFRAME CREDITO DEDFLACIONADO
# AQUI SIGO O MESMO PRINCIPIO DA VARIACAO MENSAL, CRIO UMA NOVA COLUNA CHAMADA VARIACAO TRIMESTRAL
# E CALCULO A RAZÃO ENTRE O VALOR ATUAL DA COLUNA SALDO TOTAL REAL E O VALOR DA MESMA TRÊS PERIODOS ATRAS (TRIMESTRALMENTE)
# UTILIZANDO O LAG
# DEPOIS SUBTRAI-SE POR 1 DO RESULTADO DA RAZÃO E MULTIPLICA-SE POR 100 CONVERTENDO A VARIAÇÃO EM UMA PORCENTAGEM

var_trimestral_saldos_deflacionados <- credito_deflacionado %>%
  mutate(variacao_trimestral_saldo_total = ((`saldo_total_real` / 
                                         lag(`saldo_total_real`,
                                             3)) -1) * 100)




var_trimestral_saldos_deflacionados <- var_trimestral_saldos_deflacionados %>%
  mutate(variacao_trimestral_pessoas_juridicas_real = ((`saldo_pj_real` / 
                                               lag(`saldo_pj_real`,
                                                   3)) -1) * 100)




var_trimestral_saldos_deflacionados <- var_trimestral_saldos_deflacionados %>%
  mutate(variacao_trimestral_pessoas_fisicas_real = ((`saldo_pf_real` / 
                                            lag(`saldo_pf_real`,
                                                3)) -1) * 100)




# AQUI REALIZO A ATUALIZAÇÃO DO DATAFRAME, SELECIONANDO AS COLUNAS IMPORTANTES PARA O MEU CONTEXTO
var_trimestral_saldos_deflacionados <- var_trimestral_saldos_deflacionados %>%
  select("data","variacao_trimestral_saldo_total",
         "variacao_trimestral_pessoas_juridicas_real",
         "variacao_trimestral_pessoas_fisicas_real")






#######################################################################################################################################################################################################################################
##############################################################################################################################################################################################################################################



# CALCULO VARIACAO 12 MESES VARIAVEIS SALDO DEFLACIONADO

# AGORA CALCULAMOS A VARIAÇÃO PERCENTUAL ANUAL DO CREDITO DEFLACIONADO
# SEMPRE CRIANDO UM NOVO DATAFRAME A PARTIR DE CREDITO DEFLACIONADO
# O MUTATE REALIZANDO A CRIAÇÃO DA NOVA COLUMA VARIACAO 12 MESES
# CALCULAMOS A RAZÃO ENTRE O VALOR ANUAL DA COLUNA E O VALOR DA MESMA DOZE PERIODOS ATRAS (ANUALMENTE)
# UTILIZANDO O LAG, E DEPOIS SUBTRAI-SE 1 DO RESULTADO DA RAZÃO E MULTIPLICA POR 100 PARA CONVERTER A VARIAÇÃO EM UMA PORCENTAGEM



var_12_meses_saldos_deflacionados <- credito_deflacionado %>%
  
  mutate(variacao_12_meses_saldo_total = ((`saldo_total_real` / 
                                       lag( `saldo_total_real`,
                                            12)) - 1) * 100)




var_12_meses_saldos_deflacionados <- var_12_meses_saldos_deflacionados %>%
  
  mutate(variacao_12_meses_pessoas_juridicas_real = ((`saldo_pj_real` / 
                                             lag( `saldo_pj_real`,
                                                  12)) - 1) * 100)




var_12_meses_saldos_deflacionados  <-  var_12_meses_saldos_deflacionados %>%
  
  mutate(variacao_12_meses_pessoas_fisicas_real = ((`saldo_pf_real` / 
                                         lag( `saldo_pf_real`,
                                              12)) - 1) * 100)



# REALIZAÇÃO DO SELECT E ATUALIZAÇÃO DO DATAFRAME DAS VARIAÇÕES EM 12 MESES

var_12_meses_saldos_deflacionados  <- var_12_meses_saldos_deflacionados %>%
  select("data","variacao_12_meses_saldo_total",
         "variacao_12_meses_pessoas_juridicas_real",
         "variacao_12_meses_pessoas_fisicas_real")



##### GERANDO O ARQUIVO XLSX

# ESPECIFCANDO O CAMINHO PARA O ARQUIVO XLSX


caminho_arquivo <- "C:\\Users\\Usuario\\Desktop\\CREDITO\\BASE_CREDITO.XLSX"


# CRIANDO UM ARQUIVO XLSX

wb <- createWorkbook() # A FUNÇÃO CREATWORKBOOK CRIA UM OBJETO WORKBOOK QUE E USADO PARA MANIPULAR ARQUIVOS DO EXCEL


# CRIANDO A PRIMEIRA PLANILHA

addWorksheet(wb, sheetName = "Dados") # AQUI ADICIONAMOS UMA NOVA PLANILHA NO WORKBOOK
# A PLANILHA SERA NOMEADA COMO DADOS
writeData(wb, sheet = "Dados", x = dados) # A FUNÇÃO WRITEDATA ESCREVE OS DADOS CONTIDOS NA VARIAEL DADOS NA PLANILHA DADOS


# CRIANDO A SEGUNDA PLANILHA E REALIZANDO O MESMO PROCESSO DA PLANILHA "DADOS"

addWorksheet(wb, sheetName = "Saldos")
writeData(wb, sheet = "Saldos", x = saldos)



# CRIANDO A TERCEIRA PLANILHA

addWorksheet(wb, sheetName = "inadimplencia")
writeData(wb, sheet = "inadimplencia", x = inadiplencia)




# CRIANDO A QUARTA PLANILHA
addWorksheet(wb, sheetName = "Credito_deflacionado")
writeData(wb, sheet = "Credito_deflacionado", x = credito_deflacionado)



# CRIANDO A QUINTA PLANILHA

addWorksheet(wb, sheetName = "Variacao_mensal")
writeData(wb, sheet = "Variacao_mensal", x = variacao_mensal)


# CRIANDO A SEXTA PLANILHA

addWorksheet(wb, sheetName = "Variacao_trimestral")

writeData(wb, sheet = "Variacao_trimestral", x = variacao_trimestral)


#####

# CRIANDO A SETIMA PLANILHA

addWorksheet(wb, sheetName = "Variacao_12_meses")
writeData(wb, sheet = "Variacao_12_meses", x = variacao_12_meses)



# CRIANDO A OITAVA PLANILHA

addWorksheet(wb, sheetName = "Var_mensal_saldo_deflacionado ")
writeData(wb, sheet = "Var_mensal_saldo_deflacionado ", x = var_mensal_saldos_deflacionados)



# CRIANDO A NONA PLANILHA

addWorksheet(wb, sheetName = "Var_trim_saldo_deflacionado ")
writeData(wb, sheet = "Var_trim_saldo_deflacionado ", x = var_trimestral_saldos_deflacionados)



# CRIANDO A DECIMA PLANILHA
addWorksheet(wb, sheetName = "Var_12_saldo_deflacionado " )
writeData(wb, sheet = "Var_12_saldo_deflacionado ", x = var_12_meses_saldos_deflacionados)


# SALVANDO O ARQUIVO

saveWorkbook(wb, caminho_arquivo, overwrite = TRUE)


