### PACKAGE ---------------------
library(rvest)
library(data.table)


### SCRAPE ---------------------

#dauphine
dauphine <- lapply(2000:2018, function(j){
  x <- paste0("https://www.procyclingstats.com/race/dauphine/",j,"/gc")
  z <- read_html(x) %>%
    html_nodes(".basic.results") %>%
    html_table() %>%
    .[[2]]
  for(i in 1:nrow(z)) {
    z$Rider[i] <- gsub(z$Team[i], "", z$Rider[i])
  }
  z <- z[, c("Rnk", "Rider")]
  z$Year <- j
  names(z)[1] <- "Rnk.Dauphine"
  return(z)
}) 
names(dauphine) <- paste0("daphine_", 2000:2018)
dauphine_dt <- rbindlist(dauphine)


#tdf
tour <- lapply(2000:2018, function(j){
  x <- paste0("https://www.procyclingstats.com/race/tour-de-france/",j,"/gc")
  z <- read_html(x) %>%
    html_nodes(".basic.results") %>%
    html_table() %>%
    .[[2]]
  for(i in 1:nrow(z)) {
    z$Rider[i] <- gsub(z$Team[i], "", z$Rider[i])
  }
  z <- z[, c("Rnk", "Rider")]
  z$Year <- j
  names(z)[1] <- "Rnk.Tour"
  return(z)
}) 
names(tour) <- paste0("tour_", 2000:2018)
tour_dt <- rbindlist(tour)

dat <- merge(dauphine_dt, tour_dt, by = c("Year", "Rider"), all.x = TRUE, all.y = TRUE)


tourDeSuisse <- lapply(2000:2018, function(j){
  x <- paste0("https://www.procyclingstats.com/race/tour-de-suisse/",j,"/gc")
  z <- read_html(x) %>%
    html_nodes(".basic.results") %>%
    html_table() %>%
    .[[2]]
  for(i in 1:nrow(z)) {
    z$Rider[i] <- gsub(z$Team[i], "", z$Rider[i])
  }
  z <- z[, c("Rnk", "Rider")]
  z$Year <- j
  names(z)[1] <- "Rnk.TourDeSuisse"
  return(z)
}) 
names(tourDeSuisse) <- paste0("tourDeSuisse_", 2000:2018)
tourDeSuisse_dt <- rbindlist(tourDeSuisse)

dat <- merge(dat, tourDeSuisse_dt, by = c("Year", "Rider"), all.x = TRUE, all.y = TRUE)
write.csv(dat, "./data/data.csv",row.names = FALSE)


