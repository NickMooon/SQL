# SQL
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`Users`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Users` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `NAME` VARCHAR(45) NOT NULL,
  `PASSWORD` VARCHAR(45) NOT NULL,
  `EMAIL` VARCHAR(120) NULL,
  PRIMARY KEY (`ID`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Event`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Event` (
  `NAME` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`NAME`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`EventINFO`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`EventINFO` (
  `Date` DATETIME NOT NULL,
  `place` VARCHAR(255) NOT NULL,
  `MaxUsers` INT NOT NULL,
  `Event_NAME` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`Event_NAME`),
  CONSTRAINT `EventName`
    FOREIGN KEY (`Event_NAME`)
    REFERENCES `mydb`.`Event` (`NAME`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Access right`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Access right` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `Admin` VARCHAR(45) NOT NULL,
  `DefaultUser` VARCHAR(45) NOT NULL,
  `Performer` VARCHAR(45) NOT NULL,
  `Guest` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`ID`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Creators`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Creators` (
  `IDcreate` INT NOT NULL AUTO_INCREMENT,
  `Name` VARCHAR(250) NOT NULL,
  `Quantity` INT NOT NULL,
  `Genre` VARCHAR(45) NOT NULL,
  `Festival` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`IDcreate`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Creators_and_EventINFO`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Creators_and_EventINFO` (
  `IDcreate` INT NOT NULL,
  `Event_NAME` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`IDcreate`, `Event_NAME`),
  INDEX `fk_Creators_has_EventINFO_EventINFO1_idx` (`Event_NAME` ASC) VISIBLE,
  INDEX `fk_Creators_has_EventINFO_Creators1_idx` (`IDcreate` ASC) VISIBLE,
  CONSTRAINT `fk_Creators_has_EventINFO_Creators1`
    FOREIGN KEY (`IDcreate`)
    REFERENCES `mydb`.`Creators` (`IDcreate`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Creators_has_EventINFO_EventINFO1`
    FOREIGN KEY (`Event_NAME`)
    REFERENCES `mydb`.`EventINFO` (`Event_NAME`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Users_has_EventINFO`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Users_has_EventINFO` (
  `Users_ID` INT NOT NULL,
  `EventINFO_Event_NAME` VARCHAR(255) NOT NULL,
  PRIMARY KEY (`Users_ID`, `EventINFO_Event_NAME`),
  INDEX `fk_Users_has_EventINFO_EventINFO1_idx` (`EventINFO_Event_NAME` ASC) VISIBLE,
  INDEX `fk_Users_has_EventINFO_Users1_idx` (`Users_ID` ASC) VISIBLE,
  CONSTRAINT `fk_Users_has_EventINFO_Users1`
    FOREIGN KEY (`Users_ID`)
    REFERENCES `mydb`.`Users` (`ID`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Users_has_EventINFO_EventINFO1`
    FOREIGN KEY (`EventINFO_Event_NAME`)
    REFERENCES `mydb`.`EventINFO` (`Event_NAME`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
