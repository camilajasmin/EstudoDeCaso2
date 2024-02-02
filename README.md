# Estudo de Caso
##  BikeShop

#### Visão Geral:
A BikeShop é uma empresa especializada na venda de bicicletas e acessórios relacionados. 
Localizada em uma área urbana movimentada de Uberlândia, Minas Gerais, a empresa tem 
como objetivo oferecer uma variedade de bicicletas de alta qualidade para ciclistas de todos os 
níveis, desde iniciantes até ciclistas experientes e entusiastas.

#### Desafio:
A BikeShop está crescendo rapidamente e enfrenta desafios no gerenciamento eficiente de seu 
inventário, clientes e vendas. Atualmente, eles estão registrando essas informações 
manualmente ou usando planilhas eletrônicas, o que se tornou ineficiente e propenso a erros. 
Eles reconhecem a necessidade de um sistema de banco de dados centralizado que possa 
armazenar e gerenciar essas informações de forma mais eficaz.

#### Objetivos do Sistema de Banco de Dados:
Gerenciar o inventário de bicicletas e acessórios, incluindo detalhes como modelo, marca, 
quantidade em estoque, preço de venda e fornecedor.
Manter um registro centralizado de clientes, incluindo informações como nome, endereço, 
número de telefone, endereço de e-mail e histórico de compras.
Registrar e acompanhar as vendas de bicicletas e acessórios, incluindo detalhes como data da 
venda, produtos vendidos, preço de venda, método de pagamento e vendedor responsável.

#### Requisitos Funcionais do Sistema de Banco de Dados:
Capacidade de adicionar, atualizar e excluir itens do inventário, bem como verificar a 
disponibilidade de produtos em tempo real.
Capacidade de adicionar novos clientes, atualizar informações existentes e manter um histórico 
de suas compras anteriores.
Funcionalidade para registrar novas vendas, incluindo a associação dos produtos vendidos aos 
clientes correspondentes e a geração de recibos.
Recursos de segurança para proteger os dados do cliente e do inventário contra acesso não 
autorizado.
Capacidade de gerar relatórios de vendas, análises de estoque e dados do cliente para ajudar 
na tomada de decisões comerciais.

#### Abordagem Proposta:
A BikeShop planeja desenvolver um sistema de banco de dados personalizado usando 
tecnologias modernas de banco de dados, como MySQL ou PostgreSQL. Eles planejam 
colaborar com desenvolvedores de software especializados para projetar e implementar o 
sistema de acordo com seus requisitos específicos. O sistema será acessado por funcionários 
autorizados por meio de uma interface de usuário intuitiva, onde poderão realizar todas as 
operações necessárias de forma eficiente.

#### Benefícios Esperados:
Melhoria na eficiência operacional, permitindo que a BikeShop gerencie seu inventário, clientes 
e vendas de forma mais rápida e precisa.
Maior satisfação do cliente, oferecendo um serviço mais personalizado e mantendo um 
histórico detalhado das interações anteriores.
Melhoria na tomada de decisões comerciais com base em relatórios e análises de dados 
precisos e atualizados.
Com um sistema de banco de dados eficiente e bem projetado, a BikeShop está confiante de 
que poderá atender às demandas de seus clientes de maneira mais eficaz e continuar 
prosperando no mercado de bicicletas.

__________________________________________________

## Modelo Conceitual para o estudo de caso
!["Modelo conceitual do banco de dados da BikeShop"](modeloConceitualBikeShop.png)
## Tabela de Entidades
!["Tabela com as entidades do banco de dados da BikeShop"](tabelaEntidadeBikeShop.png)
## Modelo Lógico para o Estudo de Caso
!["Modelo conceitual do banco de dados da BikeShop"](modeloLogicoBikeShop.png)

### Código SQL para o modelo físico do banco de dados
_________________________________________________________

```sql
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
DROP SCHEMA IF EXISTS `mydb` ;

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
SHOW WARNINGS;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`FORNECEDORES`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`FORNECEDORES` (
  `idFORNECEDORES` INT NOT NULL AUTO_INCREMENT,
  `nomeFornecedor` VARCHAR(50) NOT NULL,
  `enderecoFornecedor` VARCHAR(150) NOT NULL,
  `numTelefoneFornecedor` VARCHAR(15) NOT NULL,
  `emailFornecedor` VARCHAR(50) NOT NULL,
  PRIMARY KEY (`idFORNECEDORES`),
  UNIQUE INDEX `emailFornecedor_UNIQUE` (`emailFornecedor` ASC) VISIBLE)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`INVENTARIO`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`INVENTARIO` (
  `idINVENTARIO` INT NOT NULL AUTO_INCREMENT,
  `modelo` VARCHAR(50) NOT NULL,
  `marca` VARCHAR(20) NOT NULL,
  `quantidade` INT NOT NULL,
  `preco` DECIMAL(10,2) NOT NULL,
  `idFORNECEDORES` INT NOT NULL,
  PRIMARY KEY (`idINVENTARIO`, `idFORNECEDORES`),
  INDEX `fk_INVENTARIO_FORNECEDORES_idx` (`idFORNECEDORES` ASC) VISIBLE,
  CONSTRAINT `fk_INVENTARIO_FORNECEDORES`
    FOREIGN KEY (`idFORNECEDORES`)
    REFERENCES `mydb`.`FORNECEDORES` (`idFORNECEDORES`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`CLIENTES`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`CLIENTES` (
  `idCLIENTES` INT NOT NULL AUTO_INCREMENT,
  `nome` VARCHAR(50) NOT NULL,
  `endereco` VARCHAR(150) NOT NULL,
  `numTelefone` VARCHAR(15) NOT NULL,
  `email` VARCHAR(50) NOT NULL,
  PRIMARY KEY (`idCLIENTES`),
  UNIQUE INDEX `email_UNIQUE` (`email` ASC) VISIBLE)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`FUNCIONARIOS`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`FUNCIONARIOS` (
  `idFUNCIONARIOS` INT NOT NULL,
  `nomeFuncionario` VARCHAR(50) NOT NULL,
  `cargo` VARCHAR(50) NOT NULL,
  `salario` DECIMAL(10,2) NOT NULL,
  `dataAdmissao` DATE NOT NULL,
  PRIMARY KEY (`idFUNCIONARIOS`))
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`VENDEDORES`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`VENDEDORES` (
  `idVENDEDORES` INT NOT NULL AUTO_INCREMENT,
  `nomeVendedor` VARCHAR(50) NOT NULL,
  `idFUNCIONARIOS` INT NOT NULL,
  PRIMARY KEY (`idVENDEDORES`, `idFUNCIONARIOS`),
  INDEX `fk_VENDEDORES_FUNCIONARIOS1_idx` (`idFUNCIONARIOS` ASC) VISIBLE,
  CONSTRAINT `fk_VENDEDORES_FUNCIONARIOS1`
    FOREIGN KEY (`idFUNCIONARIOS`)
    REFERENCES `mydb`.`FUNCIONARIOS` (`idFUNCIONARIOS`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`VENDAS`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`VENDAS` (
  `idVENDAS` INT NOT NULL AUTO_INCREMENT,
  `data` DATETIME NOT NULL DEFAULT current_timestamp(),
  `quantidadeVendida` INT NOT NULL,
  `precoTotal` DECIMAL(10,2) NOT NULL,
  `metodoPagamento` VARCHAR(30) NOT NULL,
  `idCLIENTES` INT NOT NULL,
  `idVENDEDORES` INT NOT NULL,
  PRIMARY KEY (`idVENDAS`, `idCLIENTES`, `idVENDEDORES`),
  INDEX `fk_VENDAS_CLIENTES1_idx` (`idCLIENTES` ASC) VISIBLE,
  INDEX `fk_VENDAS_VENDEDORES1_idx` (`idVENDEDORES` ASC) VISIBLE,
  CONSTRAINT `fk_VENDAS_CLIENTES1`
    FOREIGN KEY (`idCLIENTES`)
    REFERENCES `mydb`.`CLIENTES` (`idCLIENTES`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_VENDAS_VENDEDORES1`
    FOREIGN KEY (`idVENDEDORES`)
    REFERENCES `mydb`.`VENDEDORES` (`idVENDEDORES`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

-- -----------------------------------------------------
-- Table `mydb`.`VENDAS_has_INVENTARIO`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`VENDAS_has_INVENTARIO` (
  `VENDAS_idVENDAS` INT NOT NULL,
  `VENDAS_CLIENTES_idCLIENTES` INT NOT NULL,
  `VENDAS_VENDEDORES_idVENDEDORES` INT NOT NULL,
  `INVENTARIO_idINVENTARIO` INT NOT NULL,
  `INVENTARIO_idFORNECEDORES` INT NOT NULL,
  PRIMARY KEY (`VENDAS_idVENDAS`, `VENDAS_CLIENTES_idCLIENTES`, `VENDAS_VENDEDORES_idVENDEDORES`, `INVENTARIO_idINVENTARIO`, `INVENTARIO_idFORNECEDORES`),
  INDEX `fk_VENDAS_has_INVENTARIO_INVENTARIO1_idx` (`INVENTARIO_idINVENTARIO` ASC, `INVENTARIO_idFORNECEDORES` ASC) VISIBLE,
  INDEX `fk_VENDAS_has_INVENTARIO_VENDAS1_idx` (`VENDAS_idVENDAS` ASC, `VENDAS_CLIENTES_idCLIENTES` ASC, `VENDAS_VENDEDORES_idVENDEDORES` ASC) VISIBLE,
  CONSTRAINT `fk_VENDAS_has_INVENTARIO_VENDAS1`
    FOREIGN KEY (`VENDAS_idVENDAS` , `VENDAS_CLIENTES_idCLIENTES` , `VENDAS_VENDEDORES_idVENDEDORES`)
    REFERENCES `mydb`.`VENDAS` (`idVENDAS` , `idCLIENTES` , `idVENDEDORES`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_VENDAS_has_INVENTARIO_INVENTARIO1`
    FOREIGN KEY (`INVENTARIO_idINVENTARIO` , `INVENTARIO_idFORNECEDORES`)
    REFERENCES `mydb`.`INVENTARIO` (`idINVENTARIO` , `idFORNECEDORES`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

SHOW WARNINGS;

SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

```

